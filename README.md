#include <stdio.h>
#include <conio.h>
#include <stdlib.h>
#include <dos.h>   // for delay()

void main()
{
    int i, n, window = 4;
    int base = 1;

    clrscr();
    randomize();

    printf("Enter total number of frames: ");
    scanf("%d", &n);

    while(base <= n)
    {
        printf("\nSending frames: ");

        for(i = base; i < base + window && i <= n; i++)
            printf("%d ", i);

        delay(1000);

        // Simulate frame loss
        if(rand() % 3 == 0)
        {
            printf("\nFrame %d lost!", base + 1);
            printf("\nGo-Back-N: Resending from frame %d...", base);
            delay(1000);
        }
        else
        {
            printf("\nAcknowledgment received up to frame %d", i - 1);
            base = i;
        }
    }

    printf("\n\nAll frames sent successfully (Go-Back-N ARQ)");

    getch();
}
