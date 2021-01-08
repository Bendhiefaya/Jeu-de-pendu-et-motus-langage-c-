# Jeu-de-pendu-et-motus-langage-c-
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#include <string.h>
#include<conio.h>


int choixJeu;

char tabNomJou[100][30]={};
int tabScoreJou[100]={};
void tri(int [],char [][30]);

int n;
int nombreCase(int[]);

char pseudo[30];
int compJou(char[30]);

int checkMot(char[10],char[10]);
int checkChar(char[1]);
int compteur;
int i,score;

int scorePlayer(int);
void classement();
void verScore(char[30]);

int choixPendu;
void jeuPendu();
void jeuMotus();
char penduTab[][10]={"SCHOOL","HAPPY","LEGEND","SPORT","COMEDY","CLOWN","CAR","LOVE","CARE","BULLET"};
int penduTabRand;
void menuPendu();
void menuMotus();




int main(){


	printf("||---------------------------------------------||\n");
	printf("||---------------------------------------------||\n");
	printf("||               Bienvenu au jeu               ||\n");
	printf("||---------------------------------------------||\n");
	printf("||---------------------------------------------||\n\n\n\n");




	do{
		printf("||-----------------------------------------------------||\n");
		printf("||-----------------------------------------------------||\n");
		printf("||               Veuillez choisir un jeu               ||\n");
		printf("||-----------------------------------------------------||\n");
		printf("||-----------------------------------------------------||\n");
		printf("||                     1-Le pendu                      ||\n");
		printf("||                     2-Motus                         ||\n");
		printf("||-----------------------------------------------------||\n");
		printf("||-----------------------------------------------------||\n");
		printf("||                     3-Quitter                       ||\n");
		printf("||-----------------------------------------------------||\n");
		printf("||-----------------------------------------------------||\n\n\n");

		printf("||-----------------------------------------------------||\n");
		scanf("%d", &choixJeu);
		printf("||-----------------------------------------------------||\n\n\n");
		system("cls");
		switch(choixJeu)
    	{
        	case 1:
        		printf("Le pendu \n");
        		menuPendu();
        	break;
        	case 2:
        		printf("Bienvenu au jeu motus \n");
        		menuMotus();
        	break;
			case 3:
				printf("||----------------------------------------------------------------||\n");
				printf("||----------------------------------------------------------------||\n");
				printf("||                          Au revori !                           ||\n");
				printf("||----------------------------------------------------------------||\n");
				printf("||----------------------------------------------------------------||\n");
            	break;
            default :
            	printf("Choix n'est pas valid \n");
        }
    }while(choixJeu != 3);

	return 0;

}

void menuPendu(){
	int i;

	do{
		printf("Entrer votre pseudo : ");
    	scanf("%s", &pseudo);
    	if(compJou(pseudo) == 1){
    		system("cls");
    		printf("Pseudo deja existe.\n");
		}
	}while(compJou(pseudo) == 1);

    n = nombreCase(tabScoreJou);

	tabScoreJou[n]=-1;
	strcpy(tabNomJou[n], pseudo);

	n = nombreCase(tabScoreJou);

    jeuPendu();

	do{
		printf("             1-Rejouer \n");
		printf("             2-Verifier score \n");
		printf("             3-Classement \n");
		printf("             4-Retour au menu principal \n");
		printf("             5-Quitter \n");
		scanf("%d", &choixPendu);
		system("cls");
		switch(choixPendu)
    	{
        	case 1:
        		printf("Rejouer \n");
        		jeuPendu();
        		break;
        	case 2:
        		verScore(pseudo);
        		break;
			case 3:
				classement();
        		break;
            case 4:
            	printf("Retour au menu principal \n");
            	break;
            case 5:
				printf("||----------------------------------------------------------------||\n");
				printf("||----------------------------------------------------------------||\n");
				printf("||                          Au revori !                           ||\n");
				printf("||----------------------------------------------------------------||\n");
				printf("||----------------------------------------------------------------||\n");
            	exit( EXIT_SUCCESS );
            default :
            	printf("Choix n'est pas valid \n");
        }
    }while(choixPendu != 4);

}

void jeuPendu(){

	int i,j,fc=1;
	clock_t t;

	char alpha[100]="A	B	C	D	E	F	G	H	I	J	\nK	L	M	N	O	P	Q	R	S	T\nU	V	W	X	Y	Z \n";

	char chn[]="*";
	char ch[10]="";

	char MotTab[10];
	char MotTabEto[10];

	char choixLettre[1];
	compteur = 7;

	srand(time(NULL));
	penduTabRand = rand() % 10;

	i=0;
	while(i< strlen(penduTab[penduTabRand]) )
	{
	    strcat(ch, chn);
	    i++;
	}

	printf("Bienvenu dans PENDU %s \n",pseudo);

	for(i=0;i<strlen(penduTab[penduTabRand]);i++){
		MotTab[i]=penduTab[penduTabRand][i];
	}

	for(i=0;i<strlen(penduTab[penduTabRand]);i++){
		MotTabEto[i]='*';
	}

	t = clock();


	do{
		int time_taken = ((int)clock() - t)/CLOCKS_PER_SEC;
		if(time_taken > 70){
			printf("Temps est ecoule, vous avez perdu la partie \n");
			score= 0 ;
			printf("Votre score est %d \n",score);
			break;
		}
		printf("Il vous reste %d coups a jouer et %d secondes \n",compteur,70-(clock() - t)/CLOCKS_PER_SEC);
		printf("Quel est le mot secret ? %s\n",ch );
		printf("%s ",alpha);
		printf("Taper '?' pour help \n" );
		printf("Proposez une lettre : " );

		do{
		scanf(" %s",&choixLettre);
		if(checkChar(choixLettre) == 1){
    		printf("Il faut que votre proposition composee de 1 caracteres et ne contient pas des nombres !\n");
		}
		}while(checkChar(choixLettre) == 1);


		if(choixLettre[0]=='?' && fc==1){
			compteur++;
			char cr = penduTab[penduTabRand][rand() % strlen(penduTab[penduTabRand])];
			printf("%c \n",cr);
			for(j=0;j<strlen(penduTab[penduTabRand]);j++){
				if(MotTab[j]==cr){
					MotTabEto[j]=cr;
					ch[j]=cr;
				}
			}
			for(j=0;j<strlen(alpha);j++){
				if(alpha[j]==cr){
					alpha[j]='-';
				}
			}
			fc--;
		}
		if(strchr(penduTab[penduTabRand],choixLettre[0]) != NULL){
			for(j=0;j<strlen(penduTab[penduTabRand]);j++){
				if(MotTab[j]==choixLettre[0]){
					MotTabEto[j]=choixLettre[0];
					ch[j]=choixLettre[0];
				}
			}
			for(j=0;j<strlen(alpha);j++){
				if(alpha[j]==choixLettre[0]){
					alpha[j]='-';
				}
			}
		}
		else{
			compteur = compteur-1;
		}


		time_taken = ((int)clock() - t)/CLOCKS_PER_SEC;
		//printf("%d \n",time_taken);

		if(time_taken == 70){
			printf("Temps est ecoule, vous avez perdu la partie \n");
			score= 0 ;
			break;
		}

		if(strcmp(ch,penduTab[penduTabRand]) == 0){
			break;
		}

		}while(compteur != 0);


	if(compteur == 0){
		printf("Vous avez perdu la partie");
		score = 0;
		printf("Votre score est %d \n",score);
	}
	if(strcmp(ch,penduTab[penduTabRand]) == 0){
		printf("Vous avez gagne %s !Le mot secret etait bien : %s . \n",pseudo,penduTab[penduTabRand]);
		score = scorePlayer(7-compteur);
		if(fc==0){
			score--;
		}
		printf("Votre score est %d \n",score);
	}



	for(i=0;i<n;i++){
		if(strcmp(tabNomJou[i],pseudo) == 0){
			if(score > 0 && tabScoreJou[i]!=-1){
				tabScoreJou[i] = tabScoreJou[i]+score;
				}
			else if(score > 0 && tabScoreJou[i]==-1){
				tabScoreJou[i] = tabScoreJou[i]+score+1;
			}
		}
	}

}

void menuMotus(){

    do{
		printf("Entrer votre pseudo : ");
    	scanf("%s", &pseudo);
    	if(compJou(pseudo) == 1){
    		system("cls");
    		printf("Pseudo deja existe.\n");
		}
	}while(compJou(pseudo) == 1);

    n = nombreCase(tabScoreJou);


	tabScoreJou[n]=-1;
	strcpy(tabNomJou[n], pseudo);

	n = nombreCase(tabScoreJou);


    jeuMotus();

	do{
		printf("             1-Rejouer \n");
		printf("             2-Verifier score \n");
		printf("             3-Classement \n");
		printf("             4-Retour au menu principal \n");
		printf("             5-Quitter \n");
		scanf("%d", &choixPendu);
		system("cls");
		switch(choixPendu)
    	{
        	case 1:
        		printf("Rejouer \n");
        		jeuMotus();
        		break;
        	case 2:
        		verScore(pseudo);
        		break;
			case 3:
				classement();
        		break;
            case 4:
            	printf("Retour au menu principal \n");
        		break;
            case 5:
				printf("||----------------------------------------------------------------||\n");
				printf("||----------------------------------------------------------------||\n");
				printf("||                          Au revori !                           ||\n");
				printf("||----------------------------------------------------------------||\n");
				printf("||----------------------------------------------------------------||\n");
            	exit( EXIT_SUCCESS );
            default :
            	printf("Choix n'est pas valid \n");
        }
    }while(choixPendu != 4);

}

void jeuMotus(){

	int i,j,fc=1;
	clock_t t;
	char chn[]="-";
	char ch[10]="";

	char MotTab[10];
	char MotTabEto[10];
	char MotVide[10]="";

	char choixMot[10];
	compteur = 7;

	srand(time(NULL));
	penduTabRand = rand() % 10;

	i=1;
	ch[0]=penduTab[penduTabRand][0];
	while(i< strlen(penduTab[penduTabRand]) )
	{
	    strcat(ch, chn);
	    i++;
	}

	i=0;
	while(i< strlen(penduTab[penduTabRand]) )
	{
	    strcat(MotVide, " " );
	    i++;
	}

	printf("Bienvenu MOTUS %s \n",pseudo);

	for(i=0;i<strlen(penduTab[penduTabRand]);i++){
		MotTab[i]=penduTab[penduTabRand][i];
	}

	t = clock();
	do{
		int time_taken = ((int)clock() - t)/CLOCKS_PER_SEC;
		if(time_taken > 70){
			printf("Temps est ecoule, vous avez perdu la partie \n");
			score = 0;
			printf("Votre score est %d \n",score);
			break;
		}

		printf("Il vous reste %d coups a jouer et %d secondes \n",compteur,70-(clock() - t)/CLOCKS_PER_SEC);
		printf("- %s [%s] Donner votre proposition composee de %d caracteres          ",ch,MotVide,strlen(ch) );
		do{
		scanf(" %s",&choixMot);

		if(choixMot[0]=='?'){
			for(i=0;i<strlen(ch)-1;i++){
				strcat(choixMot, " " );
			}
		}

		if(checkMot(choixMot,ch) == 1){
    		printf("Il faut que votre proposition composee de %d caracteres et ne contient pas des nombres !\n",strlen(ch) );
		}
		}while(checkMot(choixMot,ch) == 1);


		if(choixMot[0]=='?' && fc==1){
			compteur++;
			char cr = penduTab[penduTabRand][rand() % strlen(penduTab[penduTabRand])];
			printf("%c \n",cr);
			for(j=0;j<strlen(penduTab[penduTabRand]);j++){
				if(MotTab[j]==cr){
					MotTabEto[j]=cr;
					ch[j]=cr;
				}
			}
			fc--;
		}
			for(j=1;j<strlen(penduTab[penduTabRand]);j++){
				for(i=1;i<strlen(penduTab[penduTabRand]);i++){
					if(MotTab[j]==choixMot[i] && i==j){
						ch[i]=MotTab[j];

					}
					if(MotTab[j]==choixMot[i] && i!=j){
						MotVide[j]=MotTab[j];
					}
				}

			}
		compteur = compteur - 1;
		time_taken = ((int)clock() - t)/CLOCKS_PER_SEC;
		//printf("%d \n",time_taken);

		if(time_taken == 70){
			printf("Temps est ecoule, vous avez perdu la partie \n");
			score = 0;
			printf("Votre score est %d \n",score);
			break;
		}

		if(strcmp(ch,penduTab[penduTabRand]) == 0){
			break;
		}
		}while(compteur != 0);


	if(compteur == 0){
		printf("Vous avez perdu le partie");
		score = 0;
		printf("Votre score est %d \n",score);
	}
	if(strcmp(ch,penduTab[penduTabRand]) == 0){
		printf("BIEN JOUE %s ! ",pseudo);
		score = scorePlayer(6-compteur);
		printf("Votre score est %d \n",score);
	}


	for(i=0;i<n;i++){
		if(strcmp(tabNomJou[i],pseudo) == 0){
			if(score > 0 && tabScoreJou[i]!=-1){
				tabScoreJou[i] = tabScoreJou[i]+score;
				}
			else if(score > 0 && tabScoreJou[i]==-1){
				tabScoreJou[i] = tabScoreJou[i]+score+1;
			}
		}
	}

}

int scorePlayer(int ten){
	int res;

	switch(ten){
		case 0:
			res = 4;break;
		case 1:
			res = 4;break;
		case 2:
			res = 3;break;
		case 3:
			res = 3;break;
		case 4:
			res = 2;break;
		case 5:
			res = 2;break;
		case 6:
			res = 1;break;
	}
	return res;

}

int nombreCase(int tab[]){
	int nb=0,i=0;

	do{
		if(tab[i] != NULL){
			nb++;
			i++;
		}
	}while(tab[i] != NULL);

	return nb;
}

int compJou(char ch[30]){
	int i,res=0;

	for(i=0;i<n;i++){
		if(strcmp(tabNomJou[i],ch) == 0){
			res=1;
		}
	}

	return res;
}

void verScore(char ch[30]){
	int i;
	printf("-------------------- VOTRE SCORE -------------------- \n");
	printf("---------- Pseudo          Score          ---------- \n");

	for(i=0;i<n;i++){
		if(strcmp(tabNomJou[i],ch) == 0){
		printf("---------- %s          ",tabNomJou[i]);
		if(tabScoreJou[i] == -1){
			printf("%d          ---------- \n",0);
		}else{
			printf("%d          ---------- \n",tabScoreJou[i]);
		}

		}
	}
	printf("\n\n\n");


}

void classement(){
	int i;


	tri(tabScoreJou,tabNomJou);
	printf("-------------------- CLASSEMENT -------------------- \n");
	printf("---------- Pseudo          Score          ---------- \n");

	for(i=0;i<n;i++){
		printf("---------- %s          ",tabNomJou[i]);
		if(tabScoreJou[i] == -1){
			printf("%d          ---------- \n",0);
		}else{
			printf("%d          ---------- \n",tabScoreJou[i]);
		}
	}
	printf("\n\n\n");


}

int checkMot(char cm[10],char c[10]){
	int i,res=0;

	for(i=0;i<strlen(cm);i++){
		if(cm[i]>='0' && cm[i]<='9'){
			res = 1;
		}
		if(cm[i]>='a'&&cm[i]<='z'){
            res=1;
		}
	}

	if( strlen(cm) != strlen(c) ){
		res = 1;
	}
	return res;

}

int checkChar(char c[1]){

	int i,res=0;

	if( strlen(c) > 1 ){
		res = 1;
	}

	if( c[0] == ' '){
		res = 1;
	}

	if(c[0]>='0' && c[0]<='9'){
			res = 1;
		}
    if(c[0]>='a'&&c[0]<='z'){
        res=1;
    }

	return res;

}


void tri(int tab[],char tabc[][30]){
	int i,j,max,aide;
	char aidec[30];

	for (i=0; i<n-1; i++)
     {
      /* Recherche du maximum à droite de A[I] */
      max=i;
      for (j=i+1; j<n; j++)
          if (tab[j]>tab[max]) max=j;
      /* Echange de A[I] avec le maximum */
      aide=tab[i];
      tab[i]=tab[max];
      tab[max]=aide;

      strcpy(aidec,tabc[i]);
      strcpy(tabc[i],tabc[max]);
      strcpy(tabc[max],aidec);
     }

}



