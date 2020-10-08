# practica02Estructuras
Uso de Estructuras#include<stdio.h>
#include<string.h>
#define ELEMENTOS 30
struct automovil{
	int agencia;
	char marca[14];
	char subMarca[14];
	int anio;
	char kilometros[10];
	char color[8];
};

struct automovil carros[ELEMENTOS];
int i,j;
char cadenaBuscadora[14];

void agregarCoche(){
	FILE *archivo;
	archivo=fopen("AGENCIA.txt", "a+");
	printf("\n * * * INGRESE LOS DATOS DEL COCHE * * *\n");
	
	fflush(stdin);
	printf("\n\tAGENCIA: ");
	scanf("%d", &carros[i].agencia);
	fprintf(archivo, "%d\t\t", carros[i].agencia);
	printf("\n");

	fflush(stdin);
	printf("\n\tMARCA: ");
	scanf("%s", carros[i].marca);
	fprintf(archivo, "%s\t\t", carros[i].marca);
	printf("\n");
	
	fflush(stdin);
	printf("\n\tSUBMARCA: ");
	scanf("%s", carros[i].subMarca);
	fprintf(archivo, "%s\t\t", carros[i].subMarca);
	printf("\n");
	
	fflush(stdin);
	printf("\n\tANIO: ");
	scanf("%d", &carros[i].anio);
	fprintf(archivo, "%d\t\t", carros[i].anio);
	printf("\n");
	
	fflush(stdin);
	printf("\n\tKILOMETRAJE: ");
	scanf("%s", carros[i].kilometros);
	fprintf(archivo, "%s\t\t", carros[i].kilometros);
	printf("\n");
	
	fflush(stdin);
	printf("\n\tCOLOR: ");
	scanf("%s", carros[i].color);
	fprintf(archivo, "%s\n", carros[i].color);
	printf("\n* * * LOS DATOS SE HAN GUARDO * * *\n\n");
	i++;
	
	fclose(archivo);
}

void mostrarInventario(){
	FILE *archivo;
    
	archivo=fopen ("AGENCIA.txt", "r");
	char c;
    printf ("\n");
    while(feof(archivo)==0){
    c=getc(archivo);
    putchar(c);}
    putchar('\n');
    fclose(archivo);
    printf ("\n\n");
}

void buscarAgencia(){//no hace nada, me regresa al menu
	
	FILE *archivo;
		int n;
        archivo=fopen ("AGENCIA.txt", "r");
        printf ("\n");
		printf(" * * * Ingrese el numero correspondiente a la agencia a buscar: ");
		printf("\n\n\t1.- Naucalpan.\n\t2.- Coyoacan.\n\t3.-Nezahualcoyotl.\n\t4.- San Angel.\n");
		scanf("%d", &n);
		for (j=0;j<=ELEMENTOS;j++){
			if (n==carros[i].agencia){
				fscanf(archivo, "%d", carros[i].agencia);
				printf("%d\n",carros[i].agencia);
				fscanf(archivo, "%s", carros[i].marca);
				printf("%s\n",carros[i].marca);
				fscanf(archivo, "%s", carros[i].subMarca);
				printf("%s\n",carros[i].subMarca);
				fscanf(archivo, "%s", carros[i].anio);
				printf("%s\n",carros[i].anio);
				fscanf(archivo, "%s", carros[i].kilometros);
				printf("%s\n",carros[i].kilometros);
				fscanf(archivo, "%s", carros[i].color);
				printf("%s\n",carros[i].color);
			}
		}
		fclose(archivo);
		printf("\n\n");
}

void buscarMarca(){ //me devuelve al menu principal, itera una vez y da fin, llega hasta agregar marca
	char cadenaBuscadora[14]; 
	FILE *archivo;
	archivo=fopen("AGENCIA.txt","r");
	printf(" * * * Ingrese el nombre de la marca: ");
    fflush(stdin);
	fgets(cadenaBuscadora,20,stdin);
	for(i=0;i<=ELEMENTOS;i++){
		if(strcmp(carros[i].marca, cadenaBuscadora)==0){
			printf("* * * MARCA ECONTRADA * * *");
			fscanf(archivo, "%d", carros[i].agencia);
 			printf("%d",carros[i].agencia);
			fgets(carros[i].marca, 14, archivo);
 			printf("%s", carros[i].marca);
 			fgets(carros[i].subMarca, 14, archivo);
 			printf("%s", carros[i].subMarca);
 			fscanf(archivo, "%d", carros[i].anio);
 			printf("%d",carros[i].anio);
 			fgets(carros[i].kilometros, 10, archivo);
 			printf("%s", carros[i].kilometros);
 			fgets(carros[i].color, 8, archivo);
 			printf("%s", carros[i].color);
		}	else{
			printf("* * * MARCA NO ENCONTRADA * * *\n\n");}
        }
        fclose(archivo);
		printf("\n\n");
}

int main(){
	int opcion;
	FILE *archivo;
	archivo=fopen("AGENCIA.txt", "r");
	printf("\t\t* * BIENVENIDO AL REGISTO DE AUTOS * *\n");
	do{
		printf("ELIGE LA OPCION QUE DESEA REALIZAR\n\n");
		printf("\t1. AGREGAR UN AUTO.\n\t2. MOSTRAR INVENTARIO.");
		printf("\n\t3. MOSTRAR POR SUCURSAL.\n\t4. MOSTRAR POR MARCA.");
		printf("\n\t5. SALIR.\n");
		scanf("%d", &opcion);
		switch(opcion){
			case 1: 
				agregarCoche();
			break;
			case 2:
				if(archivo==NULL){
					fclose(archivo);
					printf("\n\n* * EL REGISTRO ESTA VACIO * *\n");	
				}	else{
					fclose(archivo);
					mostrarInventario();}
			break;
			case 3:
				if(archivo==NULL){
					fclose(archivo);
					printf("\n\n* * EL REGISTRO ESTA VACIO * *\n");	
				}	else{
					fclose(archivo);
					buscarAgencia();}//funcion a revisar
			break;
			case 4:
				if(archivo==NULL){
					fclose(archivo);
					printf("\n\n* * EL REGISTRO ESTA VACIO * *\n");	
				}	else{
					fclose(archivo);
					buscarMarca();}//funcion a revisar
			case 5:
				printf("\n* * * HASTA PRONTO * * *");
			break;
			default: 
				fclose(archivo);
                printf ("\n * * * * La opcion valida. * * * * \n");	}
	}while(opcion!=5);
return 0;
}
