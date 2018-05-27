# teamwork-tienda-cosmetica
teamwork-tienda-cosmetica created by GitHub Classroom


// El trabajo lo hemos realizado Carmen Blanco, Belén Escribano e Irene Cristobal.

//TIENDA COSMETICA
#include<stdio.h>
#include <string.h>


//Estructura de informacion de los productos
typedef struct{

	char nombre[30];
	int precio, codigo;

}producto;


//Estructura de contacto para el registro
typedef struct {

	int   edad, codigopostal, telefono;
	char nombre[20], apellido[20], usuario[20], correo[100], calle[50], password1[20], password2[20];

}contacto;


//Estructura tipo cuenta
typedef struct{

	char usuario[20], password[9];

}cuenta;


//Prototipos de las funciones
void Registro(contacto c1);
void Compra(producto *v);


// Codigo main
void main(){

	char op, categoria, menu, reclamacion[1000];

	FILE *f;

	int i=0, j, k, tecla, codigo;

	char usuario[20]="oscar", passw[10]="1234";
	char login[20],cont[10];
	int intento=0;

	cuenta acceso[20];

	contacto c;

	// Se definen cuatro estructuras para almacenar los productos y sus respectivos codigos y precios.
	producto datosM[3]={ {"1 pintalabios",20,1}, {"2 colorete",18,2}, {"3 mascara de pestaï¿½as",25,3} };
	producto datosP[3]={ {"1 champu",14,1}, {"2 acondicionador",16,2}, {"3 mascarilla",19,3} };
	producto datosR[3]={ {"1 crema hidratante",50,1}, {"2 tonico",40,2}, {"3 agua micelar",35,3} };
	producto datosC[3]={ {"1 vainilla",60,1}, {"2 coco",40,2}, {"3 floral",180,3} };

	printf("ï¿½Bienvenido a nuestra tienda de cosmetica!\n\n");

	do{

		printf("Si ya tiene cuenta, pulse A para acceder, en caso contrario pulse B para registrarse\n\n");

		scanf("%c", &op);

		switch (op) {

			case 'A': // ACCESO
			case 'a':

				do{
					printf("Usuario: ");
					scanf("%s",login);

					printf("Contraseï¿½a: ");
					scanf("%s",cont);

					if(strcmp(login,usuario)!=0 || strcmp(cont,passw)!=0){
						printf("Usuario o clave incorrectos.\n");
					}
					intento++;
					if(intento==3){
						printf("Ha superado el maximo numero de intentos\n");
						return -1;
					}


				}while(strcmp(usuario,login)!=0||(strcmp(passw,cont))!=0);

				break;

			case 'B': // EN CASO DE NO TENER CUENTA, SE PROCEDE AL REGISTRO
			case 'b':
				Registro(c);
				break;

			default: printf("Opcion incorrecta\n\n");
				break;
		}
	} while(op!='A'&&op!='B'&&op!='a'&&op!='b');


	//PAGINA WEB

	printf("Bienvenido al area de clientes. \n\n ");

	printf("Menu: \n\n");

	do{

		printf("Productos (p)\n Contacto (c)\n Reclamaciones (r)\n\n");

		scanf("%c",&menu);

		switch(menu){
			case'p':
			case 'P':
				do{

					printf("Seleccione una categoria:\n\n");
					printf("m: Maquillaje \n c: Cabello \n r: Rostro \n p: Perfumes \n\n ");
					scanf("%c",&categoria);

					switch(categoria){

						case'm':
						case 'M':
							printf(" A continuaciï¿½n, se muestra una lista de los productos disponibles\n\n");
							for(i=0;i<3;i++){
								printf("%s\n",datosM[i].nombre);
							}
							printf("\n");
							printf("Si desea comprar algun producto pulse 1\n\n");
							scanf("%d", &tecla);

							if(tecla==1){
								Compra(datosM);
								printf("Su pedido se enviara a la calle registrada");
							}

								break;
						case'c':
						case 'C':
							printf(" A continuaciï¿½n, se muestra una lista de los productos disponibles\n");
							for(i=0;i<3;i++){
								printf("%s\n",datosC[i].nombre);
							}
							printf("\n");

							printf("Si desea comprar algun producto pulse 1, \n\n");
							scanf("%d", &tecla);

							if(tecla==1){
								Compra(datosC);
								printf("Su pedido se enviara a la calle registrada");
							}

								break;
						case'r':
						case 'R':
							printf("A continuaciï¿½n, se muestra una lista de los productos disponibles\n\n");
							for(i=0;i<3;i++){
								printf("%s\n",datosR[i].nombre);
							}
							printf("\n");

						    printf("Si desea comprar algun producto pulse 1, \n\n");
							scanf("%d", &tecla);


							if(tecla==1){
								Compra(datosR);
								printf("Su pedido se enviara a la calle registrada");
							}

								break;
						case'p':
						case 'P':
							printf(" A continuaciï¿½n, se muestra una lista de los productos disponibles\n\n");
							for(i=0;i<3;i++){
								printf("%s\n",datosP[i].nombre);
							}
							printf("\n");
							printf("Si desea comprar algun producto pulse 1, \n\n");
							scanf("%d", &tecla);

							if(tecla==1){
								Compra(datosP);
								printf("Su pedido se enviara a la calle registrada");
							}

								break;
						/*default:
							printf("ERROR\n");
							break;*/

					}



					}while(categoria!='m'&&categoria!='r'&&categoria!='c'&&categoria!='p');
				break;
			case'c':
			case 'C':
				printf("En caso de dudas o problemas, puede contactar con nosotros a traves de nuestro correo electronico o telefono\n\n");
				printf("Correo: duditas@cosmeticalia.com\n\n");
				printf("Telefono: 900304050\n\n");
				break;
			case'r':
			case 'R':
				f=fopen("Reclamaciones.txt","w");

				if(f==NULL){
					printf("Lo sentimos. No se ha podido realizar la reclamaciï¿½n\n\n");
					break;
				}

				printf("Por favor, escriba su reclamacion:\n\n"); // LA RECLAMACION SE GUARDA EN UN FICHERO DE TEXTO
				fflush(stdin);
				fgets(reclamacion,1000,stdin);

				fprintf(f,"%s",reclamacion);

				printf("Muchas gracias \n\n");

				fclose(f);
				break;
			/*default: printf("ERROR\n");*/
		}

	} while(menu!='p'&& menu!='c'&& menu!='r');
}

// FUNCIONES

void Registro(contacto c1) {
	int orden1;

	int i;


	cuenta personas[1]={"oscar","1234"};

		printf("Rellene los siguientes datos para poder registrarse: \n");
		printf("Nombre: ");
		scanf("%s", c1.nombre);
		printf("Apellido: ");
		scanf("%s", c1.apellido);
		printf("Edad: ");
		scanf("%d",&c1.edad);
		printf("Calle: ");
		scanf("%s",c1.calle);
		printf("Codigo postal: ");
		scanf("%d",&c1.codigopostal);
		printf("Telefono: ");
		scanf("%d",&c1.telefono);
		printf("Correo electronico: ");
		scanf("%s", c1.correo);

		do {                                        //compara el usuario introducido con el usuario que tenemos guardado, en caso de que coincidan lo volverï¿½ a pedir
		                                           //hasta que no coincida

				printf("Nombre de usuario:\n ");
				scanf("%s", c1.usuario);


				} while ((strcmp(c1.usuario, personas[0].usuario)==0) || (strcmp(c1.usuario, personas[1].usuario)==0));


		do{

			printf("Crea tu contraseï¿½a: ");
			scanf("%s", c1.password1);
				while(strlen(c1.password1)>8){        //La contraseï¿½a no puede tener mas de ocho caracteres, si los tiene la volverï¿½ a pedir.
					printf("La contraseï¿½a es demasiado larga, vuelva a introducirla:\n");
					scanf("%s", c1.password1);
					}

			     printf("Repita la contraseï¿½a: ");
			    scanf("%s", c1.password2);


			orden1 = strcmp(c1.password1, c1.password2);  //compara las dos contraseï¿½as introducidas
			if(orden1!=0){
				printf("Las contraseï¿½as no coinciden, pruebe de nuevo por favor\n.\n");
			}


			else{
				printf("Contraseï¿½a guardada.\n"); //una vez registrado puede iniciar la compra
			}

	}
		while(orden1!=0);

}


void Compra(producto *v){

	int card,cvv,precio;
	producto p;

	printf("Indique el codigo del producto que desea comprar: \n\n");
	scanf("%d", &p.codigo);

	precio=v[p.codigo-1].precio;
	printf("El precio del producto es %d euros \n\n",precio);
	printf("Introduzca el numero de su tarjeta de credito:\n\n");
	scanf("%d",&card);
	printf("Introduzca su CVV: \n\n");
	scanf("%d",&cvv);
	printf("Gracias por su compra.\n\n");


}
