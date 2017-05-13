#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#define gridSize 4
/*recursive fonksiyon kullanilmistir.*/
/*#define DEBUG*/

typedef enum {
	closedEmpty=0,
	empty=1,
	closedMined=2,
	flaggedMined=3,
	mined=4,
	flaggedEmpty=5
}cell;

int isCellEmpty(cell grid[][gridSize], int x, int y);
void initGrid(cell grid[][gridSize]);
int isLocationLegal(int x, int y);
void printGrid (cell grid[][gridSize]);
void flagCell(cell grid[][gridSize], int x, int y);
int openCell(cell grid[][gridSize], int x, int y);
void minesweeper(cell grid[][gridSize]);
void neighbor(cell grid[][gridSize],int x, int y);
int countEmptyCell(cell grid[][gridSize]);
int openMined(cell grid[][gridSize]);
int asMain();

int main()
{	
	asMain();

}
int asMain()
{

	cell grid[gridSize][gridSize];
	initGrid(grid);
	
	printf("Welcome to minesweeper game. \nFirst you should enter the location and then you will enter the move.\n");
	printf("f : for flag the cell of reflag the cell.\no : for open the cell.\n");
	printGrid(grid);
	minesweeper(grid);
	return 1;
}

void minesweeper(cell grid[][gridSize])
{
	/*oyunun ana fonksiyonudur. tüm islemler burada gerceklesir diger fonksiyonlar burada cagirilir.*/
	int move=0,lost=1;
	int x=0,y=0;
	char d;
	int empty=0;
	empty = countEmptyCell(grid);
	/*printf("x: %d y: %d\n",x,y );*/
	
	while(empty != 0 && lost != 0)
	{
		printf("Please enter the location x and y = \n");
		scanf("%d %d",&x,&y);
		printf("Please enter 'o'(for open) or 'f'(for flag) : \n");
		scanf(" %c",&d);	

		if(isLocationLegal(x,y) == 1)
		{
			move++;
			if(isCellEmpty(grid,x,y) == 1)
			{
				/*lokasyonun bos ve legal oldugunu kontrol ettikten sonra kullanici open derse openCell flag derse flagCell fonksiyonu cagirilir.*/
				if(d == 'o')
				{
					openCell(grid,x,y);	
				}
				else if(d == 'f')
					flagCell(grid,x,y);		
				else
					printf("Wrong character.\n");

			}

			else
			{
				if(grid[x][y] == closedMined)
				{

					if(d=='f')
						flagCell(grid,x,y);
					else
					{
						lost=0;
					}
					/*eger mayin  varsa flag veya lose sonucunu verir.*/
				}

				else
				{	/*önceden flag varsa açmayıp flag kaldırılacak.*/
					if(d == 'o')
						printf("Please first reflag the location.\n");
					else
						flagCell(grid,x,y);	 			
				}

			}

		}
		else 
		{
			printf("The location is not correct.\n");
			return;
		}
		empty = countEmptyCell(grid);
		if(lost != 0)
			printGrid(grid);
	}
	
	if(lost == 0)
	{
		openMined(grid);
		printf("GAME OVER.\nYou have %d moves.\n",move);
	}
	else
		printf("Congratulations! You win the game with %d moves.\n",move);

}

void initGrid(cell grid[][gridSize])
{
	/*is a function to initialize your matrix as an arbitrary initial game board
	 with closed-empty and closed-mined cells.*/
	int size = (gridSize * gridSize) -1; 
	int k=0,number=0;
	int i=0,j=0;
	const int sizeConst = size;
	int normal;
	/*cell arr[255] = {closedEmpty, closedMined,closedMined,closedEmpty,closedEmpty,closedEmpty,closedMined,closedMined,closedEmpty,closedEmpty,closedEmpty,closedEmpty,closedEmpty,closedEmpty,closedEmpty,closedEmpty};*/
	normal = (int)(gridSize * gridSize) / 4;
	/*int easy,hard;
	easy = (int)(gridSize * gridSize) / 8;
	hard = (int)(gridSize * gridSize) / 2;*/
	
	/*oyunun zorluk derecesini ayarlamak icin 3 tane deger olusturdum. Ama fonksiyona 
	alabilmek icin gerekli parametre yoktu sonraya biraktim. kare matrixin icini rand fonksiyonu ile
	rasgele dolduruyorum. stdlib ve time.h onun icin gerekli. suan icin sadece mayin sayisini azaltmak icin kullanıyorum.*/


	srand(time(NULL));
	number = rand();
	while(k<=size)
	{
		number = rand() % 3;
		if(number == 0 || number == 2)
		{
			if(normal %2 == 0 && number == 2)
			{
				arr[k] = number;
				k++;
				normal--;
				
			}
			else if(number == 0 )
			{
				arr[k] = number;
				k++;
				normal--;
			}
		}
	
	}

	for (i = 0; i < gridSize; ++i)
	{
		for (j = 0;j  < gridSize; ++j)
		{
			grid[i][j] = arr[size] ;
			size--;/*k yı size -- olarak degistir*/
		}
		printf("\n");
	}
}

int isCellEmpty(cell grid[][gridSize], int x, int y)
{
	/*return value int result=0 if the cell is not an empty cell and result=1 the cell is an empty cell.*/
	/*lokasyon bos ise return 1 yapıyor.*/
	if(grid[x][y] == empty || grid[x][y] == closedEmpty)
		return 1;
	else 
		return 0;

}

int isLocationLegal(int x, int y)
{
	/*return value int result=0 if the location is illegal and result=1 if the location is legal(in the grid).*/
	/*girilen lokasyon matrixin boyutundan buyuk olup olmadigini kontrol ediyor. yanlis buyukluk girilirse return 0 doner.*/
	if((x >= gridSize || x < 0) || (y >= gridSize || y < 0))
		return 0;
	else 
		return 1;

}

void printGrid (cell grid[][gridSize])
{
	int line,gridSize2,i=1,satir,x=0,y=0;

	gridSize2 = gridSize;
	line = (2*gridSize) +1;
	satir = line;
	
	/*olusturdugumuz matrixi ekrana bastırma. satir ve sütundaki cizgilerin icine mayin veya bos oldugunu bastiriyor.*/
	while(line>0)
	{
		if(line%2==1)
		{
			for (i = 0; i < satir; ++i)
			{
				printf("--");
			}	
			printf("\n");
		}

		else
		{
			printf("|");
			while(gridSize2>0)
			{	
				if(grid[x][y] == closedEmpty || grid[x][y] == closedMined)
					/*printf(" . |");*/
					printf(" %d |",grid[x][y]);
				/*yukarıdaki printf i nerelerde mayin oldgunu ogrenebilmek icin acabilirsiniz.*/
				else if(grid[x][y] == empty)
					printf(" e |");
				else if(grid[x][y] == flaggedMined || grid[x][y] == flaggedEmpty)
					printf(" f |");
				else if(grid[x][y] == mined)			
					printf(" M |");
	
				gridSize2--;
				y++;
			}
			x++;
			y=0;
			gridSize2 = gridSize;
			printf("\n");
		}

		line--;
	}

}

void flagCell(cell grid[][gridSize], int x, int y)
{
	/*if a cell is wanted to be flagged; check 
	if it is empty or mined: if it is empty, flag as flagged-empty;
	 if it is mined, flag as flagged-mined*/
	
	/*kordinat bos veya kapali mayin ise direk olarak flag atiyor. degilse flag varsa onceden flagi geri aliyor. */
	if(isCellEmpty(grid,x,y) == 1)
	{
		#ifdef DEBUG
		fprintf(stderr, "t-old:%d\n",grid[x][y]);
		#endif		
		grid[x][y] = flaggedEmpty;
		printf("%d\n",grid[x][y] );
	}
	else 
	{	
		/*there is a mined or turn back.*/
		if(grid[x][y] == closedMined)
		{
			grid[x][y] = flaggedEmpty;
			#ifdef DEBUG
			fprintf(stderr, "t-new:%d\n",grid[x][y]);
			#endif			
		}
		else if(grid[x][y] == flaggedMined )
		{
			grid[x][y] = closedMined;
			#ifdef DEBUG
			fprintf(stderr, "t-chance:%d\n",grid[x][y]);
			#endif		
		}

		else if (grid[x][y] == flaggedEmpty)
			grid[x][y] = closedEmpty;
	}

}

int openCell(cell grid[][gridSize], int x, int y)
{
	if((x<0 || x>=gridSize) || (y<0 || y>=gridSize))
		return 0;
	if(grid[x][y] == closedEmpty)
	{
		grid[x][y] = empty;

		
		return 1 + openCell(grid,x-1,y)+
		openCell(grid,x+1,y)+
		openCell(grid,x,y-1)+
		openCell(grid,x,y+1);
	}
	else return 0;

}
/*
void neighbor(cell grid[][gridSize], int x, int y)
{
	 bellirli cell in komsularinin bos olup olmadigini bul.
	int i,j;

	for(i = x - 1; i <= x + 1; i++)
	{
		for(j = y - 1; j <= y + 1; j++)
		{
			if( isLocationLegal(i,j) != 0)
			{
				if(isCellEmpty(grid,i,j) == 1)
				{
					grid[i][j] = empty;
				}
			}

		}

	}

}*/

int countEmptyCell(cell grid[][gridSize])
{
	int empty=0;
	int i=0,j=0;
	/*tablodaki tum bos cell leri hesapliyor. eger bos sayilar bitmezse oyun bitmiyor. flagler oncesinde bos ise oyun devam ediyor.*/
	for (i = 0; i < gridSize; ++i)
	{
		for (j = 0;j  < gridSize; ++j)
		{
			if(grid[i][j] == closedEmpty || grid[i][j] == flaggedMined)
				empty++;
		}
	}

	/*printf("empty cell: %d\n",empty );*/
	return empty;

}

int openMined(cell grid[][gridSize])
{
	int i=0,j=0;

	for(i=0;i<gridSize;i++)
	{
		for(j=0;j<gridSize;j++)
		{
			if(grid[i][j] == closedMined)
			{
				grid[i][j] = mined;
			}

		}

	}
	printGrid(grid);
	return 1;
}
