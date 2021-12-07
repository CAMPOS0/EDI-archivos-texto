# Archivos de texto

Utilizando archivos de texto en C, escriba un programa que capture y guarde en un archivo de texto
los nombres y calificaciones de los alumnos de una materia.  Además deberá calcular el promedio de 
los alumnos en el archivo:

1.  Realice una función capture el nombre y calificación de los alumnos de una materia y los guarde en un archivo.
2.  Realice una función lea la información del archivo y calcule el promedio de los alumnos.

El programa deberá preguntar el número de alumnos en la clase y de acuerdo a eso capturarlos o leerlos.



#include <stdio.h>
#include <stdlib.h>

#define N 5
#define nomTam 20

void leeClase(int tam);
void imprime(int tam);

int main()
{
    int salon;
    printf("Cuantos alumnos son? ");
    scanf("%d",&salon);
    leeClase(salon);
    imprime(salon);
}

void leeClase(int tam)
{
    FILE *ptr;
    int i;
    float cal;
    char name[nomTam];

    ptr=fopen("cal.txt","w");

    if(ptr==NULL)
    {
        printf("Error: No existe el archivo cal.txt");
        exit(0);
    }

    for(i=0;i<tam;i++)
    {
        printf("Nombre %d: ",i);
        scanf("%s",name);
        printf("Calificacion %d: ",i);
        scanf("%f",&cal);
        fprintf(ptr,"%s %f",name,cal);
    }
    fclose(ptr);
}

void imprime(int tam)
{
    FILE *ptr;
    int i;
    float acum=0,x;
    char name[nomTam];

    ptr=fopen("cal.txt","r");

if(ptr==NULL)
    {
        printf("Error: No existe el archivo cal.txt");
        exit(0);
    }

    while(!feof(ptr))
    {
        fscanf(ptr,"%s",name);
        fscanf(ptr,"%f",&x);

        acum = acum + x;
    }

    fclose(ptr);
    acum = acum / tam;
    printf("El promedio de los alumnos es de: %f",acum);
}
