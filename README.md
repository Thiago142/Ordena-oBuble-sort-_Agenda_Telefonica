# Ordena-oBuble-sort-_Agenda_Telefonica
Agenda -Telefonica-ComOrdenaãoBubleSort

#include <stdio.h>
#include <stdlib.h>
#include <string.h>
//Função abaixo esta pegando como parametro de entrada um vetor de caracteres para nome e um sequencia de inteiros de 9 digitos
void registra(char nome[50], double telefone)
{
    FILE *fd; // declarando variavel de um arquivo.
    fd=fopen("nomesagenda.txt","a"); //abertura de um arquivo e anexando ou escrevendo no final do arquivo de acordo com o "a"-;
    fprintf(fd, "%s\n", nome);// mostrar  nome dentro do arquivo
    fprintf(fd, "%lf\n", telefone);// mostrar telefone dentro do arquivo
    printf("\n Dados registrados!\n\n");
    printf(" Pressione enter para voltar ao menu de opcoes!");
    fclose(fd); //fechamento de arquivo.
    getchar(); // lê um caracter e retorna um inteiro que é o código do caracter, ou o valor -1 que corresponde a fim de ficheiro.
}
//Função que faz a pesquisa de acordo com os usuarios/contatos registrados na função acima.
void pesquisa(char pesq[])
{
    FILE *fd; //declaração da variavel de arquivo.
    char curs[50];// tamanho de nomes
    double telefone;// varivel em forma de double para poder armazenar de 9 digitos
    int existe=0;
    fd=fopen("nomesagenda.txt","r"); //abrindo o arquivo criado e utilizando a função "r" que siginifica "leitura" para acessá-lo.
    while ((fgets(curs, sizeof(curs), fd))!=NULL) //enquanto minha string ou seja o nome digitado para pesquisa dentro do arquivo for diferente de NULL e faz o processo abaixo.
        if (strcmp(curs, pesq)) //Se minha a comparação entre a string armazenada e a string digitada for iguais o programa reconhece e printa na tela o contato.
        {
            printf("\n Nome: %s", curs);
            fscanf(fd,"\n%lf", &telefone);
            printf("\n Telefone: %9.lf\n", telefone);
            fscanf(fd,"\n");
            existe++;
        }
        else
        {
            fscanf(fd,"\n\n");// Caso não ele lê o arquivo novamente.
        }
    if (existe!=0)
    {
        printf("\n Cadastro nao encontrado ou inexistente!\n");
    } //Se existir não existir nenhuma condição verdadeira do primeiro if, ou seja, a string que o usuario nao estiver no arquivo o contato é inexistente.
    printf("\n Pressione enter para voltar ao menu de opcoes!");
    getchar();
    fclose(fd); // fechamento do arquivo.
}
//Função que faz a listagem de todos os contados entrados pelo usuarios e que foram salvos no arquivo criado.
void listar()
{
    FILE *fd; //declarando variavel para o arquivo.
    char curs[50];
    double telefone;
    int i=0;
    fd=fopen("nomesagenda.txt","r"); //abertura do arquivo para leitura atraves da função "r" de read.
    while ((fgets(curs,sizeof(curs), fd))!=NULL)//enquanto minha string ou seja o nome digitado para pesquisa dentro do arquivo for diferente de NULL faz o processo abaixo.
    {
        printf(" \n Nome: %s",curs); //printa o nome
        fscanf(fd,"\n%lf", &telefone); //leitra do telefone do arquivo.
        printf(" \n Telefone: %9.lf\n", telefone); //printa o telefone lido.
        fscanf(fd,"\n"); // leitura de uma linha dentro do arquivo.
        i++; // acrescento 1 para cada contato exibido
    }
    printf(" \n Total de contatos registrados: %d\n",i);
    printf(" \n Pressione enter para voltar ao menu de opcoes!");
}
//Função que faz a exclusao de todos os contatos armazenados dentro de um arquivo.
void listalimp()
{
    FILE *fd;//declaração de variavel de arquivo.
    char opcao;
    printf(" Seus contatos todos serao apagados, deseja realmente continuar (S/N)? ");
    scanf("%c", &opcao);
    if(opcao=='s' || opcao=='S')
    {
        fd=fopen("nomesagenda.txt","w+");//Abertura do arquivo tanto para leitura como para escrita caso já exista o arquivo, seu conteúdo será substituído.
        printf("\n Contatos apagados com sucesso!\n\n ");
        printf(" Pressione enter para voltar ao menu de opcoes!");
        getchar();
    }
    else
    {
        if(opcao=='n' || opcao=='N')
        {
            printf(" Pressione enter para voltar ao menu de opcoes!");
        }
    }
    fclose(fd);
    getchar();// lê um caracter e retorna um inteiro que é o código do caracter, ou o valor -1 que corresponde a fim de ficheiro.

}
void ordena()//procedimento ordenar opção 5 do  switch case
{
    FILE *fd;// ponteiro do arquivo
    int contreg=0;// variavel para contar registro
    double *vet;// ponteiro para ser alocando dinamicamente
    double tam=100;//tamnanho do vetor  que ele poderá armazenar os contatos.

    vet=(double*)malloc(tam*sizeof(double));// Alocando  a minha variavel vet  dinamicamente para guarda os telefones do 0 ate 99
    // poderiamos ter allocado  usnado também  com  calloc, nele a unica diferença e que podemos alocar e ja colocar o tamanho nescessario para armazenar
    // não precisando criar outra variavel  para fazer o tamanho igual o exemplo acima .
    //double *vet;//vet[contreg];
    //vet=(double *)calloc(100,sizeof(double));
    double telefone,aux;// variavel telefone double para pode armazenar numero maior que 9 digitos , variavel aux para guardar  os telefones na hora da ordenação
    char nomes[50];// variavel  para guarda uma string  de ate 50 caracteres.
    char vnomes[100][50];// vetor para guarda  100 nomes  de tamanho 50 caracter
    int i=0,j=0;// variavel de controle

    if(vet==NULL) // verificando se o tamanho alocado no meu vetor deu erro ou memoria insuficiente na hora de ser alocado ,
    {
        printf("Erro memoria insuciente ");
    }
    fd=fopen("nomesagenda.txt","r");//abrindo o meu arquivo fd  para leitura

    while ((fgets(nomes,sizeof(nomes), fd))!=NULL)//enquanto minha string ou seja o nome digitado para pesquisa dentro do arquivo for diferente de NULL faz o processo abaixo.
    {
        printf(" \n Nome: %s",nomes);// mostrando  todos os nomes  antes de ser ordenados
        fscanf(fd,"\n%lf", &telefone);// salvando   os telefones  dentro do meu arquivo

        vet[i]=telefone;//Guardando  os telefenes no meu vetor então em cada possição de i ele guardará  um telefone diferente
        strcpy(vnomes[contreg],nomes);//  copiando  os nomes para um vetor que estar contando registro  então em cada possição do meu vetor ele
        // guarda um nome diferente dentro do meu vetor.
        contreg ++;//conta registro a cada registro  acrescenta 1
        i ++;// contador do telefone a cada telefone acrescenta 1

        printf(" \n Telefone: %9.lf\n", telefone); //mostra na tela  os telefone lido.
        fscanf(fd,"\n");// pula de linha dentro do meu arquivo
    }
    fclose(fd);// fechar o arquivo
    printf("\n \t \tTELEFONES   ORDENADOS :\n");// Aviso para mostrar os  telefones ordenados
    for( i=0; i<contreg; i++ )// for para começar  ordenar desde do 1 telefone ate o ultimo , nesse ele começar  do 1
    {
        for( j=i+1; j<contreg; j++ )// ja nesse for ele começa no segundo telefone ou seja na segunda posiçao por causa do i +1 então
            // estar sempre comparando uma possição a mais,essa comparação e para comparar pares de elemento
            // tipo posição i=0, telefone [0], j=i+1, então compara telefone[0]com telefone [1].
        {
            if( vet[i] > vet[j] )// comparação para começar pegando o telefone que tem o menor ddd  o uso do sinal do maior vai estar percorrendo
                // e me trazendo o telefone com ddd menor
            {
                aux = vet[i];// fazendo com que a minha variavel aux guarde o telefone na possição i para não perde o valor na troca
                vet[i] = vet[j];// ja com valor de vet[i] guardado  eu armazeno então o segundo telefone nela
                vet[j] = aux;// O meu vetor vet[j] agora pasará a receber o primeiro telefone , isso quer dizer que o telefone da 1 posição e maior do que estar na segunda então acontece a troca
                strcpy(nomes, vnomes[i]);// copiando  o meu vetor de nome na posição nomes para que depois na hora da troca os nomes não sai errado
                strcpy(vnomes[i],vnomes[j]);// copiando o meu segundo nome para  o primeiro
                strcpy(vnomes[j],nomes);// depois eu pego primeiro nome e jogo para a segunda posição
            }
        }
        printf("\nNome: %s",vnomes[i]);// mostro todos nomes guardados no  meu vetor
        printf("Telefone: %9.lf\n",vet[i]);// mostro todos os telefones guardados
    }
    printf("\n");//pula linha
    printf("\n");
    printf("Telefones Ordenado  Por DDD com sucesso! \n");// Aviso para mostrar os telefones ordenador
    free(vet);// liberando o array apos ele ter sido usando,caso eu não libere depois de ter usando ele estará com a memoria cheia e vai travar
    // o meu programa falando que as posição ja estão com conteudo armazenado , e sempre importante quando fazendo alocação dinamica  liberar esse
    // conteúdo armazenado dentro das  variaveis.
}
int main(void)
{
    FILE *fd; //variavel de arquivo criada assim como nas outras funções;
    int menu,tamnome;//variaveis de controle para execução das funções
    double telefone; //declarei double para armazenar mais numeros
    char nome[50]; //vetor de caracteres para guardar um nome
    while (menu!=0) //enquanto minha opção do menu for diferente de zero executa o programa abaixo.
    {
        printf("\n----------- Agenda de telefones !!-------------\n");
        printf("\n 1-- Registrar contato.");
        printf("\n 2-- Procurar contato.");
        printf("\n 3-- Listar contatos.");
        printf("\n 4-- Limpar lista de contatos.");
        printf("\n 5-- Ordenar por DDD seus contatos.");
        printf("\n 6-- Informacoes adicionais.");
        printf("\n\n 0- Sair.");
        printf("\n\n Opcao: ");
        scanf("%d",&menu); //leitura de opção de acordo com os printf's acima
        getchar();// lê um caracter e retorna um inteiro que é o código do caracter, ou o valor -1 que corresponde a fim de ficheiro.
        switch (menu) //de acordo com a opção digitada no menu o switch toma uma decisão.
        {
        case 1:
        {
            printf("\n Entre com um nome (no maximo de 50 letras): \n ");
            gets(nome); //leitura de um nome num vetor.
            tamnome=strlen(nome); //tamanho do nome recebe o tamanho do vetor de caracteres passado pelo usuario
            if (tamnome>50) //se o tamanho for maior do que 50 posições ele printa a mensagem abaixo.
            {
                printf("O tamanho do nome do seu contato ultrapassa de 50 letras.\n");
                getchar();
                getchar();
            }
            else //caso não ele pede o telefone do usuario.
            {
                printf(" Entre com o DDD e telefone. Ex: (45992132435)\n ");
                scanf("%lf",&telefone); //leitura do telefone
                getchar();
                registra(nome, telefone); // chamada da função para registrar o nome e um telefone.
            }
        }
        break;
        case 2:
        {
            printf("\n Entre com um nome (no maximo de 50 letras): \n ");
            gets(nome);  //leitura de um nome num vetor.
            tamnome=strlen(nome);//tamanho do nome recebe o tamanho do vetor de caracteres passado pelo usuario.
            if (tamnome>50) //se o tamanho for maior do que 50 posições ele printa a mensagem abaixo.
            {
                printf("O tamanho do nome do seu contato ultrapassa de 50 letras.\n");
                getchar();
                getchar();
            }
            else //caso não ultrapasse ele faz a chamada da função
            {
                pesquisa(nome);
            }
        }
        break;
        case 3:
        {
            listar(); //chamada de função para listagem de contatos.
            getchar();
        }
        break;
        case 4:
        {
            listalimp(); //chamada da função para apagar todos contatos.
        }
        break;
        case 5:
        {
            ordena();
            printf(" \n Pressione enter para voltar ao menu de opcoes!");
            getchar();
        }
        break;
        case 6:
        {
            printf(" \n Agenda criada por: \n\n  Lenon Henrique.\n  Joao Ricardo.\n  Thiago Antonio.\n  Rafael Miranda.\n  ");
            printf(" \n\n Pressione enter para voltar ao menu de opcoes!");
            getchar();
        }
        break;
        case 0:
            break;
        default: //caso usuario digite algum numero incoveniente e fora das opções do menu ele printa a informação abaixo.
        {
            printf("\n Opcao invalida..\n");
            printf(" \n Pressione enter para voltar ao menu de opcoes!");
            getchar();
        };
        }
    }
    return(0); //retorna 0.
}


