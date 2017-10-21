#include<stdio.h>
#include <iostream>
#include <string.h>
#include <stdlib.h>
#include <time.h>

int main(){
	srand(time(NULL));
	const int MAX = 52;
	char deck [MAX];
	int aux = 1;
	int cartasIniciales = 2;
	
	for (int i = 0; i < MAX;){
	
		switch(aux){
		case 10:for (int x = 0; x < 4; x++){
				deck[i] = 'J';
				i++;		
			}
			break;
		case 11:for (int x = 0; x < 4; x++){
				deck[i] = 'K';
				i++;		
			}
			break;
		case 12:for (int x = 0; x < 4; x++){
				deck[i] = 'Q';
				i++;		
			}
			break;
		case 13:for (int x = 0; x < 4; x++){
				deck[i] = 'A';
				i++;		
			}
			break;
		default:
			for (int x = 0; x < 4; x++){
				deck[i] = aux + '0';
				i++;		
			}
			break;
		}
				aux++;
		
	}		
	aux = 0;
	int auxiliar[MAX];
	char deckReborujado[MAX];
	bool flag = false;
	while (aux != MAX){
		int numAleatoreo = rand() % 52;
		for(int x = 0; auxiliar[x] != '\0'; x++)
			if(auxiliar [x] == numAleatoreo)
				flag = true;
		if(flag == false){
			deckReborujado[aux] = deck[numAleatoreo];
			aux++;
		}
	
	}
	char eleccion;
	printf("Quieres una tercer carta? (s para si)");
	scanf("%c",&eleccion);
	int cartasEntregadas = 0,puntajeJugador = 0,puntajeComputadora = 0;	
	if(eleccion == 's')
		cartasIniciales = 3;
	char primerJugador[cartasIniciales],computadora[2] ;
	for(cartasEntregadas = 0; cartasEntregadas < cartasIniciales; cartasEntregadas++){
		primerJugador[cartasEntregadas] = deckReborujado[cartasEntregadas];
		deckReborujado[cartasEntregadas] = '0';
		if (primerJugador[cartasEntregadas] == 'J' || primerJugador[cartasEntregadas] == 'K'
			||primerJugador[cartasEntregadas] == 'Q')
			puntajeJugador += 10;
		else if(primerJugador[cartasEntregadas] == 'A'){
			int A;
			while(A != 1 && A != 11){
				printf("Salio un az!! escoge entre 1 y 11 :");
				scanf("%i",&A);
			}
			puntajeJugador += A;
		}	
		else{
			puntajeJugador += (primerJugador[cartasEntregadas] - '0');
		}
	}
	
	for(int i = 0; i < 2; i++){
		computadora[i] = deckReborujado[cartasEntregadas];
		deckReborujado[cartasEntregadas] = '0';
		cartasEntregadas++;
		if (computadora[i] == 'J' || computadora[i] == 'K'
			|| computadora[i] == 'Q')
			puntajeComputadora += 10;
		else if(computadora[i] == 'A'){
			puntajeComputadora += 11;
		}	
		else{
			puntajeComputadora += (computadora[i] - '0');
		}
	}
	printf("Puntaje de la computadora: %i\n",puntajeComputadora);
	printf("Puntaje del jugador: %i\n",puntajeJugador);
	printf("Cartas de la computadora[%s]\n",computadora);
	printf("Cartas del jugador") ;
	for(int i = 0; i < cartasIniciales; i++)	
		printf("[%c]",primerJugador[i]);
	printf("\nLas cartas del deck : %s\n",deckReborujado);
	if(puntajeComputadora <= 21 && puntajeJugador <= 21)
	{
		if(puntajeComputadora > puntajeJugador){
			printf("Gano el ordenador");
		}
		else if(puntajeComputadora == puntajeJugador){
			printf("Empate");
		}
		else{
			printf("Gano el jugador");
		}
	}
	else if(puntajeComputadora <= 21 && puntajeJugador > 21){
		printf("Gano el ordenador");
	}
	else{
		printf("Gano el jugador");
	}
	return 0;

}
