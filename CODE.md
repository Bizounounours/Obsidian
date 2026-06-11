```C
// structure

struct wavfile{
    /* Descripteur "RIFF" */
    char        chunkID[4];        
    int         chunkSize;          
    char        format[4];          

    /* Sous-bloc "fmt " (le format audio) */
    char        subchunk1ID[4];    
    int         subchunk1Size;      
    short       audioFormat;        
    short       numChannels;        
    int         sampleRate;        
    int         byteRate;          
    short       blockAlign;        
    short       bitsPerSample;      

    /* Sous-bloc "data" (le contenu audio) */
    char        subchunk2ID[4];    
    int         subchunk2Size;      
};


struct send_data
{
    struct wavfile file_h;
    int* data_tab;
    int lenght;
};


// gestion du fichier

#include <stdio.h>
#include <stdlib.h>
#include <stdint.h>
#include <string.h>
#include "file_gestion.h"

struct send_data read_wav(int nb_mot, char *mot[]) {
    if (nb_mot < 2) {
        fprintf(stderr, "Usage: %s <filename.wav>\n", mot[0]);
        exit(1);
    }

    char *filename = mot[1];
    FILE *wav = fopen(filename, "rb");
    struct wavfile header;

    if (wav == NULL) {
        fprintf(stderr, "Can't open input file %s", filename);
        exit(1);
    }

    // read header
    if (fread(&header, sizeof(header), 1, wav) < 1) {
        fprintf(stderr, "Can't read file header\n");
        exit(1);
    }

    if (header.chunkID[0] != 'R' || header.chunkID[1] != 'I' || 
        header.chunkID[2] != 'F' || header.chunkID[3] != 'F') { 
        fprintf(stderr, "ERROR: Not wav format\n"); 
        exit(1); 
    }

    fprintf(stderr, "wav format\n");

    // Adaptation pour Afficher()
    // calcule de la taille des données
    fseek(wav, 0, SEEK_END);
    long fileSize = ftell(wav);
    long dataStart = sizeof(struct wavfile); 
    long remainingBytes = fileSize - dataStart;
    
    // tableau contenant toutes les données
    int nb_sample_max = remainingBytes / sizeof(short);
    if (nb_sample_max <= 0) {
        fprintf(stderr, "Erreur : Fichier vide ou trop petit\n");
        exit(1);
    }
    
    int* tab = malloc(nb_sample_max * sizeof(int));
    if (tab == NULL) {
        fprintf(stderr, "Erreur allocation mémoire\n");
        exit(1);
    }

    // Retour au début des données (après le header de 44 octets)
    fseek(wav, dataStart, SEEK_SET);

    // read data
    short value = 0;
    int i = 0; //taille du tableau pour afficher

    while (i < nb_sample_max && fread(&value, sizeof(value), 1, wav)) {
        tab[i] = value; // On stocke pour l'affichage
        if (value < 0) { value = -value; }
        i++;
    }

    printf("Nom du bloc lu dans le header : %.4s\n", header.subchunk2ID);
    printf("Nombre d'echantillons reellement lus : %d\n", i);
    struct send_data sdata = {header, tab, i};
    
    fclose(wav);
    return sdata;
}

void write_wav() {
}


// Affichage

#include "raylib.h"
#include "Graphic.h"

int Affichage(int* tab_y, int tab_taille) {
    const int screenWidth = 2400;
    const int screenHeight = 1200;

    if (!IsWindowReady()) {
        InitWindow(screenWidth, screenHeight, "Affichage Amplitude");
    }

    float zoomX = 1.0f;
    float zoomY = 0.05f; 
    float offsetX = 0.0f;
    float offsetY = 0.0f;

    SetTargetFPS(60);

    while (!WindowShouldClose()) {
        float wheel = GetMouseWheelMove();

        if (wheel != 0) {
            if (IsKeyDown(KEY_LEFT_CONTROL) || IsKeyDown(KEY_RIGHT_CONTROL)) {
                zoomX += wheel * 0.1f * zoomX;
                if (zoomX < 0.001f) zoomX = 0.001f;
            } else {
                zoomY += wheel * 0.1f * zoomY;
                if (zoomY < 0.00001f) zoomY = 0.00001f;
            }
        }

        if (IsMouseButtonDown(MOUSE_BUTTON_LEFT)) {
            Vector2 delta = GetMouseDelta();
            offsetX -= delta.x / zoomX;
            offsetY -= delta.y / zoomY;
        }

        BeginDrawing();
            ClearBackground(RAYWHITE);
            
            int milieu = screenHeight / 2;
            float axeCentral = milieu - (offsetY * zoomY);
            
            DrawLine(0, axeCentral, screenWidth, axeCentral, LIGHTGRAY);

            int start = (int)offsetX;
            int end = start + (int)(screenWidth / zoomX) + 2;

            if (start < 0) start = 0;
            if (end > tab_taille - 1) end = tab_taille - 1;

            for (int i = start; i < end; i++) {
                float x1 = (i - offsetX) * zoomX;
                float x2 = (i + 1 - offsetX) * zoomX;
                float y1 = axeCentral + (tab_y[i] * zoomY);
                float y2 = axeCentral + (tab_y[i+1] * zoomY);

                DrawLineEx((Vector2){x1, y1}, (Vector2){x2, y2}, 1.0f, RED);
            }

            DrawRectangle(10, 10, 320, 100, Fade(SKYBLUE, 0.5f));
            DrawText(TextFormat("Hauteur (Y) : Molette (%.4f)", zoomY)
            , 20, 45, 13, BLACK);
            DrawText(TextFormat("Largeur (X) : CTRL + Molette (%.4f)", zoomX)
            , 20, 65, 13, BLACK);
            DrawText("Drag : Clic gauche", 20, 85, 11, DARKGRAY);
        EndDrawing();
    }

    CloseWindow();
    return 0;
}


// main pour test

#include <stdio.h>
#include <stdlib.h>
#include <stdint.h>
#include <string.h>
#include "Graphic.h"
#include "file_gestion.h"

int main(int argc, char *argv[]) {
    struct send_data wav_data = read_wav(argc, argv);
    int* données_tab = wav_data.data_tab;
    int taille = wav_data.lenght;

    Affichage(données_tab, taille);

    // Nettoyage à faire
    return 0;
}
```