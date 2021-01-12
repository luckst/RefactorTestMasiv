# RefactorTestMasiv

```sh
public class Printer {
    public static void main(String[] args) throws Exception {
        final int maxCount = 1000;        
        final int ordMax = 30;
        int primeNumbers[] = new int[maxCount+1];        
        int numberToValidate = 1;
        int currentPosition = 1;
        boolean isPrime;
        int ord = 2;
        int square = 9;
        int mult[] = new int[ordMax+1];
        primeNumbers[1] = 2;

        while (currentPosition < maxCount) {
            do {
                numberToValidate += 2;
                if( numberToValidate == square) {
                    ord++;
                    square=primeNumbers[ord]*primeNumbers[ord];
                    mult[ord-1]=numberToValidate;
                }

                int N=2;
                isPrime=true;
                while (N < ord && isPrime) {
                    while (mult[N]<numberToValidate)
                        mult[N] += primeNumbers[N] + primeNumbers[N];

                    if (mult[N] == numberToValidate)
                        isPrime=false;

                    N++;
                }
            } while (!isPrime);
            currentPosition++;
            primeNumbers[currentPosition]=numberToValidate;
        }

       PrintNumbers(maxCount, primeNumbers);
    }

    public static void PrintNumbers(int maxCount, int[] primeNumbers) {        
        final int RowCount = 50;
        final int ColumnCount = 4;
        int PAGENUMBER = 1;
        int PAGEOFFSET = 1;

        while (PAGEOFFSET <= maxCount) {
            PrintHeader(maxCount, PAGENUMBER);
            for (int ROWOFFSET=PAGEOFFSET; ROWOFFSET <= PAGEOFFSET+RowCount-1; ROWOFFSET++) {
                PrintColumn(RowCount, ColumnCount, maxCount, ROWOFFSET, primeNumbers);
                System.out.println();
            }
            System.out.println("\f");
            PAGENUMBER++;
            PAGEOFFSET += RowCount*ColumnCount;
        }
    }

    public static void PrintHeader(int maxCount, int PAGENUMBER) {
        System.out.print("The First ");
        System.out.print(Integer.toString(maxCount));
        System.out.print(" Prime Numbers === Page ");
        System.out.print(Integer.toString(PAGENUMBER));
        System.out.println("\n");
    }

    public static void PrintColumn(int RowCount, int ColumnCount, int maxCount, int ROWOFFSET, int[] primeNumbers) {
        for (int Column = 0; Column <= ColumnCount - 1; Column++)
            if (ROWOFFSET + Column * RowCount <= maxCount)
                System.out.printf("%10d", primeNumbers[ROWOFFSET + Column * RowCount]);
    }
}
```
