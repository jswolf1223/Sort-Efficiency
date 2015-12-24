package hw10;


import java.util.Arrays;

/**
 * A class that contains several sorting routines,
 * implemented as static methods.
 * Arrays are rearranged with smallest item first,
 * using compareTo.
 * @author Mark Allen Weiss with edits by McCauley
 * 
 * @updated Joseph Sams Wolf
 * CSCI230 Homework 10
 * Counters have been added to the sort class to find the number of 
 * data moves and data comparisons.
 * 
 */
public final class Sort
{
    
	public static int insertionMoveCount = 0; // counts number of data moves in insertion sort.
	public static int shellMoveCount = 0;  // counts number of data moves in shell sort.
	public static int heapMoveCount = 0;  // counts number of data moves in heap sort.
	public static int quickMoveCount = 0; // counts number of data moves in quick sort.
	public static int mergeMoveCount = 0;  // counts number of data moves in merge sort.
	public static int insertionCompCount = 0; //counts number of comparisons in insertion sort.
	public static int shellCompCount = 0;  //counts number of comparisons in shell sort.
	public static int heapCompCount = 0;  //counts number of comparisons in heap sort.
	public static int quickCompCount = 0;  //counts number of comparisons in quick sort.
	public static int mergeCompCount = 0;  //counts number of comparisons in merge sort.
	
	/**
     * Simple insertion sort.
     * @param a an array of Comparable items.
     */
    public static <AnyType extends Comparable<? super AnyType>>
    void insertionSort( AnyType [ ] a )
    {
        insertionMoveCount = 0; // reset
        insertionCompCount = 0; // reset
    	int j;
        for( int p = 1; p < a.length; p++ )
        {
            
        	AnyType tmp = a[ p ];
            insertionMoveCount++;
			j = p;
            while(j > 0 && tmp.compareTo( a[ j - 1 ] ) < 0 ) {
                insertionCompCount++;
            	a[ j ] = a[ j - 1 ];
                insertionMoveCount++;
			    j--;
			}
            a[ j ] = tmp;
            insertionMoveCount++;
        }
    }

    /**
     * Shellsort, using Shell's (poor) increments.
     * @param a an array of Comparable items.
     */
    public static <AnyType extends Comparable<? super AnyType>>
    void shellsort( AnyType [ ] a )
    {
        shellMoveCount = 0; // reset
        shellCompCount = 0; // reset
    	int j;
        for( int gap = a.length / 2; gap > 0; gap /= 2 )
            for( int i = gap; i < a.length; i++ )
            {
                AnyType tmp = a[ i ];
                shellMoveCount++;
                for( j = i; j >= gap &&
                            tmp.compareTo( a[ j - gap ] ) < 0; j -= gap )
                {
                	shellCompCount++;
                    a[ j ] = a[ j - gap ];
                    shellMoveCount++;
                }    
                a[ j ] = tmp;
                shellMoveCount++;
            }
    }

    
    
    /**
     * Internal method for heapsort.
     * @param i the index of an item in the heap.
     * @return the index of the left child.
     */
    private static int leftChild( int i )
    {
        return 2 * i + 1;
    }
    
    /**
     * Internal method for heapsort that is used in deleteMax and buildHeap.
     * @param a an array of Comparable items.
     * @index i the position from which to percolate down.
     * @int n the logical size of the binary heap.
     */
    private static <AnyType extends Comparable<? super AnyType>>
    void percDown( AnyType [ ] a, int i, int n )
    {
    	
    	int child;
        AnyType tmp;

        for( tmp = a[ i ]; leftChild( i ) < n; i = child )
        {
            child = leftChild( i );
            if( child != n - 1 && a[ child ].compareTo( a[ child + 1 ] ) < 0 )
            {	
                heapCompCount++;
            	child++;
            }	
            if( tmp.compareTo( a[ child ] ) < 0 )
            {
            	heapCompCount++;
            	a[ i ] = a[ child ];
            	heapMoveCount++;
            }
            else
                break;
        }
        a[ i ] = tmp;
        heapMoveCount++;
    }
    
    /**
     * Standard heapsort.
     * @param a an array of Comparable items.
     */
    public static <AnyType extends Comparable<? super AnyType>>
    void heapsort( AnyType [ ] a )
    {
        heapMoveCount = 0; // reset
        heapCompCount = 0; // reset
    	for( int i = a.length / 2 - 1; i >= 0; i-- )  /* buildHeap */
            percDown( a, i, a.length );
        for( int i = a.length - 1; i > 0; i-- )
        {
            swapReferences( a, 0, i ); /* deleteMax */
            heapMoveCount +=3;
            percDown( a, 0, i );
        }
    }


    /**
     * Mergesort algorithm.
     * @param a an array of Comparable items.
     */
    public static <AnyType extends Comparable<? super AnyType>>
    void mergeSort( AnyType [ ] a )
    {
        mergeMoveCount =0; // reset
        mergeCompCount =0; // reset
    	AnyType [ ] tmpArray = (AnyType[]) new Comparable[ a.length ];

        mergeSort( a, tmpArray, 0, a.length - 1 );
    }

    /**
     * Internal method that makes recursive calls.
     * @param a an array of Comparable items.
     * @param tmpArray an array to place the merged result.
     * @param left the left-most index of the subarray.
     * @param right the right-most index of the subarray.
     */
    private static <AnyType extends Comparable<? super AnyType>>
    void mergeSort( AnyType [ ] a, AnyType [ ] tmpArray,
               int left, int right )
    {
        if( left < right )
        {
            int center = ( left + right ) / 2;
            mergeSort( a, tmpArray, left, center );
            mergeSort( a, tmpArray, center + 1, right );
            merge( a, tmpArray, left, center + 1, right );
        }
    }

    /**
     * Internal method that merges two sorted halves of a subarray.
     * @param a an array of Comparable items.
     * @param tmpArray an array to place the merged result.
     * @param leftPos the left-most index of the subarray.
     * @param rightPos the index of the start of the second half.
     * @param rightEnd the right-most index of the subarray.
     */
    private static <AnyType extends Comparable<? super AnyType>>
    void merge( AnyType [ ] a, AnyType [ ] tmpArray, int leftPos, int rightPos, int rightEnd )
    {
        
    	int leftEnd = rightPos - 1;
        int tmpPos = leftPos;
        int numElements = rightEnd - leftPos + 1;

        // Main loop
        while( leftPos <= leftEnd && rightPos <= rightEnd )
            if( a[ leftPos ].compareTo( a[ rightPos ] ) <= 0 ) 
            	tmpArray[ tmpPos++ ] = a[ leftPos++ ];
            else 	
                tmpArray[ tmpPos++ ] = a[ rightPos++ ];
        	mergeCompCount++;
        	mergeMoveCount++;
        while( leftPos <= leftEnd )    // Copy rest of first half
            tmpArray[ tmpPos++ ] = a[ leftPos++ ];
        	mergeMoveCount++;
        while( rightPos <= rightEnd )  // Copy rest of right half
            tmpArray[ tmpPos++ ] = a[ rightPos++ ];
        	mergeMoveCount++;
        // Copy tmpArray back
        for( int i = 0; i < numElements; i++, rightEnd-- )
        {   
        	a[ rightEnd ] = tmpArray[ rightEnd ];
        	mergeMoveCount++;
        }
      
    }

    /**
     * Quicksort algorithm.
     * @param a an array of Comparable items.
     */
    public static <AnyType extends Comparable<? super AnyType>>
    void quicksort( AnyType [ ] a )
    {
    	quickCompCount = 0; // reset
    	quickMoveCount = 0; // reset
        quicksort( a, 0, a.length - 1 );
    }

    private static final int CUTOFF = 3;

    /**
     * Method to swap to elements in an array.
     * @param a an array of objects.
     * @param index1 the index of the first object.
     * @param index2 the index of the second object.
     */
    public static <AnyType> void swapReferences( AnyType [ ] a, int index1, int index2 )
    {
        AnyType tmp = a[ index1 ];
        a[ index1 ] = a[ index2 ];
        a[ index2 ] = tmp;
    }

    /**
     * Return median of left, center, and right.
     * Order these and hide the pivot.
     */
    private static <AnyType extends Comparable<? super AnyType>>
    AnyType median3( AnyType [ ] a, int left, int right )
    {
        int center = ( left + right ) / 2;
        if( a[ center ].compareTo( a[ left ] ) < 0 )
        {
            quickCompCount++;
        	swapReferences( a, left, center );
        	quickMoveCount += 3;
        }    
        if( a[ right ].compareTo( a[ left ] ) < 0 )
        {
            quickCompCount++;
            swapReferences( a, left, right );
            quickMoveCount += 3;
        }    
        if( a[ right ].compareTo( a[ center ] ) < 0 )
        {    
            quickCompCount++;
        	swapReferences( a, center, right );
        	quickMoveCount += 3;
        }

            // Place pivot at position right - 1
        swapReferences( a, center, right - 1 );
        quickMoveCount += 3;
        return a[ right - 1 ];
    }

    /**
     * Internal quicksort method that makes recursive calls.
     * Uses median-of-three partitioning and a cutoff of 10.
     * @param a an array of Comparable items.
     * @param left the left-most index of the subarray.
     * @param right the right-most index of the subarray.
     */
    private static <AnyType extends Comparable<? super AnyType>>
    void quicksort( AnyType [ ] a, int left, int right )
    {
        if( left + CUTOFF <= right )
        {
            AnyType pivot = median3( a, left, right );

                // Begin partitioning
            int i = left, j = right - 1;
            for( ; ; )
            {
                while( a[ ++i ].compareTo( pivot ) < 0 ) {quickCompCount++; }
                while( a[ --j ].compareTo( pivot ) > 0 ) {quickCompCount++; }
                if( i < j )
                {
                	swapReferences( a, i, j );
                	quickMoveCount +=3;
                }
                else
                    break;
            }

            swapReferences( a, i, right - 1 );   // Restore pivot
            quickMoveCount+=3;
            quicksort( a, left, i - 1 );    // Sort small elements
            quicksort( a, i + 1, right );   // Sort large elements
        }
        else  // Do an insertion sort on the subarray
            insertionSort( a, left, right );
    }

    /**
     * Internal insertion sort routine for subarrays
     * that is used by quicksort.
     * @param a an array of Comparable items.
     * @param left the left-most index of the subarray.
     * @param right the right-most index of the subarray.
     */
    private static <AnyType extends Comparable<? super AnyType>>
    void insertionSort( AnyType [ ] a, int left, int right )
    {
        for( int p = left + 1; p <= right; p++ )
        {
            AnyType tmp = a[ p ];
            quickMoveCount++;
            int j;

            for( j = p; j > left && tmp.compareTo( a[ j - 1 ] ) < 0; j-- )
            {    
            	quickCompCount++;
            	a[ j ] = a[ j - 1 ];
            	quickMoveCount++;
            }
            a[ j ] = tmp;
            quickMoveCount++;
        }
    }


    private static final int NUM_ITEMS = 25000;
    private static int theSeed = 1;

    /**
     * McCauley: I changed Weiss' void checkSort method
     * to a boolean isSorted method. 
     * @param a
     * @return true if a is in ascending order, false otherwise
     */
    private static boolean isSorted( Integer [ ] a )
    {
        for( int i = 0; i < a.length; i++ )
            if( a[ i ] != i )
                return false;
        return true;
    }


    /**
     * McCauley: I removed some code not related to HW10 and 
     * changed so that it only prints and exits with an error
     * if a sort does not return a sorted list.
     * 
     * Driver has been updated to find the average run time of
     * each sort type for an in order array, reverse array, and 
     * random array. The average run time for each is calculated 
     * from 5 iterations.  The average number of data comparisons
     * and data moves is also calculated for each sort type. 
     */
    public static void main( String [ ] args )
    {
    	System.out.println("Analyzing sorting algorithms (This may take a moment).");
    	
    	// Total times for each type of sort.
    	long aTime, a1Time, a2Time, a3Time, a4Time, bTime, b1Time, b2Time, b3Time, b4Time,
    	cTime, c1Time, c2Time, c3Time, c4Time;
    	
    	aTime = a1Time = a2Time = a3Time = a4Time = bTime = b1Time = b2Time = b3Time = b4Time =
    	cTime = c1Time = c2Time = c3Time = c4Time = 0;
    	
    	// Total counts for comparisons and moves for each type of sort.
    	
    	int insMove,insComp,heapMove,heapComp,shellMove,shellComp,mergeMove,mergeComp,quickMove,quickComp,
    	insMoveRev,insCompRev,heapMoveRev,heapCompRev,shellMoveRev,shellCompRev,mergeMoveRev,mergeCompRev,
    	quickMoveRev,quickCompRev, insMoveRand,insCompRand,heapMoveRand,heapCompRand,shellMoveRand,shellCompRand,
    	mergeMoveRand,mergeCompRand, quickMoveRand,quickCompRand;
    	
    	insMove=insComp=heapMove=heapComp=shellMove=shellComp=mergeMove=mergeComp=quickMove=quickComp=
    	insMoveRev=insCompRev=heapMoveRev=heapCompRev=shellMoveRev=shellCompRev=mergeMoveRev=mergeCompRev=
    	quickMoveRev=quickCompRev=insMoveRand=insCompRand=heapMoveRand=heapCompRand=shellMoveRand=shellCompRand=
    	mergeMoveRand=mergeCompRand=quickMoveRand=quickCompRand=0;
    	
    	for( int h = 0; h < 5; h++ )
        {
    		Integer [ ] a = new Integer[ NUM_ITEMS ];
    		Integer [ ] b = new Integer[ NUM_ITEMS ];
    		Integer [ ] c = new Integer[ NUM_ITEMS ];
    		// Array stores values 1..NUM_ITEMS-1
    		int j = b.length;
    		 
    		for( int i = 0; i < a.length; i++ ){
    			a[ i ] = i;  // ordered array.
    			b[ i ] = j;  // reverse order array.
    			c[ i ] = i;  // used for random array.
    			j--;
    		}
    		
    		
    		Integer [] a1 = a.clone();
    		Integer [] a2 = a.clone();
    		Integer [] a3 = a.clone();
    		Integer [] a4 = a.clone();
    		
    		Integer [] b1 = b.clone();
    		Integer [] b2 = b.clone();
    		Integer [] b3 = b.clone();
    		Integer [] b4 = b.clone();
    		
    		
    		Random.permute( c );  // random array
    		
    		// array is cloned to ensure results are not skewed by differing array distribution.
    		
    		Integer [] c1 = c.clone();
    		Integer [] c2 = c.clone();
    		Integer [] c3 = c.clone();
    		Integer [] c4 = c.clone();
    		
    		
            long aStart = System.currentTimeMillis(); // sort start time
            Sort.insertionSort( a );
            long aEnd = System.currentTimeMillis();  // sort end time
            insMove+= insertionMoveCount; insComp+=insertionCompCount;
            long bStart = System.currentTimeMillis();
            Sort.insertionSort( b );
            long bEnd = System.currentTimeMillis();
            insMoveRev+= insertionMoveCount; insCompRev+=insertionCompCount;
            long cStart = System.currentTimeMillis();
            Sort.insertionSort( c );
            long cEnd = System.currentTimeMillis();
            insMoveRand+= insertionMoveCount; insCompRand+=insertionCompCount;
            if (!isSorted(a)) {
                System.out.println("Sort failed.");
                System.exit(1);
            }
           
            long a1Start = System.currentTimeMillis();
            Sort.heapsort( a1 );
            long a1End = System.currentTimeMillis();
            heapMove+= heapMoveCount; heapComp+=heapCompCount;
            long b1Start = System.currentTimeMillis();
            Sort.heapsort( b1 );
            long b1End = System.currentTimeMillis();
            heapMoveRev+= heapMoveCount; heapCompRev +=heapCompCount;
            long c1Start = System.currentTimeMillis();
            Sort.heapsort( c1 );
            long c1End = System.currentTimeMillis();
            heapMoveRand+= heapMoveCount; heapCompRand+=heapCompCount;
             if (!isSorted(a)) {
                System.out.println("Sort failed.");
                System.exit(1);
            }

            //Random.permute( a );
            long a2Start = System.currentTimeMillis();
            Sort.shellsort( a2 );
            long a2End = System.currentTimeMillis();
            shellMove += shellMoveCount; shellComp += shellCompCount; 
            long b2Start = System.currentTimeMillis();
            Sort.shellsort( b2 );
            long b2End = System.currentTimeMillis();
            shellMoveRev += shellMoveCount; shellCompRev += shellCompCount; 
            long c2Start = System.currentTimeMillis();
            Sort.shellsort( c2 );
            long c2End = System.currentTimeMillis();
            shellMoveRand += shellMoveCount; shellCompRand += shellCompCount; 

            if (!isSorted(a)) {
                System.out.println("Sort failed.");
                System.exit(1);
            }

            //Random.permute( a );
            long a3Start = System.currentTimeMillis();
            Sort.mergeSort( a3 );
            long a3End = System.currentTimeMillis();
            mergeMove += mergeMoveCount; mergeComp += mergeCompCount;
            long b3Start = System.currentTimeMillis();
            Sort.mergeSort( b3 );
            long b3End = System.currentTimeMillis();
            mergeMoveRev += mergeMoveCount; mergeCompRev += mergeCompCount;
            long c3Start = System.currentTimeMillis();
            Sort.mergeSort( c3 );
            long c3End = System.currentTimeMillis();
            mergeMoveRand += mergeMoveCount; mergeCompRand += mergeCompCount;
             if (!isSorted(a)) {
                System.out.println("Sort failed.");
                System.exit(1);
            }
            //Random.permute( a );
            long a4Start = System.currentTimeMillis();
            Sort.quicksort( a4 );
            long a4End = System.currentTimeMillis();
            quickMove += quickMoveCount; quickComp += quickCompCount;
            long b4Start = System.currentTimeMillis();
            Sort.quicksort( b4 );
            long b4End = System.currentTimeMillis();
            quickMoveRev += quickMoveCount; quickCompRev += quickCompCount;
            long c4Start = System.currentTimeMillis();
            Sort.quicksort( c4 );
            long c4End = System.currentTimeMillis();
            quickMoveRand += quickMoveCount; quickCompRand += quickCompCount;
            if (!isSorted(a)) {
                System.out.println("Sort failed.");
                System.exit(1);
            }
            // Start time is subtracted from end time to find sort time in milliseconds.
            // These results are added to total time for each sort type.
            
            aTime += aEnd - aStart; a1Time += a1End - a1Start; a2Time += a2End - a2Start;
            a3Time += a3End - a3Start; a4Time += a4End - a4Start;
            bTime += bEnd - bStart; b1Time += b1End - b1Start; b2Time += b2End - b2Start;
            b3Time += b3End - b3Start; b4Time += b4End - b4Start;
            cTime += cEnd - cStart;c1Time += c1End - c1Start; c2Time += c2End - c2Start;
            c3Time += c3End - c3Start; c4Time += c4End - c4Start;
        }
    	
    	// Total sort time is divided by # of iterations (5) to find average time in milliseconds.
    	
    	System.out.println("Insertion sort ordered average time " + (aTime/5.0) + " milliseconds.");
    	System.out.println("Insertion sort reverse average time " + (bTime/5.0) + " milliseconds.");
    	System.out.println("Insertion sort random average time " + (cTime/5.0) + " milliseconds.");
    	System.out.println("Heap sort ordered average time " + (a1Time/5.0) + " milliseconds.");
    	System.out.println("Heap sort reverse average time " + (b1Time/5.0) + " milliseconds.");
    	System.out.println("Heap sort random average time " + (c1Time/5.0) + " milliseconds.");
    	System.out.println("Shell sort ordered average time " + (a2Time/5.0) + " milliseconds.");
    	System.out.println("Shell sort reverse average time " + (b2Time/5.0) + " milliseconds.");
    	System.out.println("Shell sort random average time " + (c2Time/5.0) + " milliseconds.");
    	System.out.println("Merge sort ordered average time " + (a3Time/5.0) + " milliseconds.");
    	System.out.println("Merge sort reverse average time " + (b3Time/5.0) + " milliseconds.");
    	System.out.println("Merge sort random average time " + (c3Time/5.0) + " milliseconds.");
    	System.out.println("Quick sort ordered average time " + (a4Time/5.0) + " milliseconds.");
    	System.out.println("Quick sort reverse average time " + (b4Time/5.0) + " milliseconds.");
    	System.out.println("Quick sort random average time " + (c4Time/5.0) + " milliseconds.\n");
    	
    	// Total comparison and move counts are divided by # of iteration (5) to find average counts.
    	System.out.println("Ordered Insertion Sort Count Averages\nMoves: " + insMove/5 +
    	" Comparisons: " + insComp/5);
    	System.out.println("Reverse Insertion Sort Count Averages\nMoves: " + insMoveRev/5 + 
    	" Comparisons: " + insCompRev/5);
    	System.out.println("Random Insertion Sort Count Averages\nMoves: " + insMoveRand/5 + 
    	" Comparisons: " + insCompRand/5);
    	System.out.println("Ordered Heap Sort Count Averages\nMoves: " + heapMove/5 + 
    	" Comparisons: " + heapComp/5);
    	System.out.println("Reverse Heap Sort Count Averages\nMoves: " + heapMoveRev/5 + 
    	" Comparisons: " + heapCompRev/5);
    	System.out.println("Random Heap Sort Count Averages\nMoves: " + heapMoveRand/5 + 
    	" Comparisons: " + heapCompRand/5);
    	System.out.println("Ordered Shell Sort Count Averages\nMoves: " + shellMove/5 + 
    	" Comparisons: " + shellComp/5);
    	System.out.println("Reverse Shell Sort Count Averages\nMoves: " + shellMoveRev/5 + 
    	" Comparisons: " + shellCompRev/5);
    	System.out.println("Random Shell Sort Count Averages\nMoves: " + shellMoveRand/5 + 
    	" Comparisons: " + shellCompRand/5);
    	System.out.println("Ordered Merge Sort Count Averages\nMoves: " + mergeMove/5 + 
    	" Comparisons: " + mergeComp/5);
    	System.out.println("Reverse Merge Sort Count Averages\nMoves: " + mergeMoveRev/5 + 
    	" Comparisons: " + mergeCompRev/5);
    	System.out.println("Random Merge Sort Count Averages\nMoves: " + mergeMoveRand/5 + 
    	" Comparisons: " + mergeCompRand/5);
    	System.out.println("Ordered Quick Sort Count Averages\nMoves: " + quickMove/5 + 
    	" Comparisons: " + quickComp/5);
    	System.out.println("Reverse Quick Sort Count Averages\nMoves: " + quickMoveRev/5 + 
    	" Comparisons: " + quickCompRev/5);
    	System.out.println("Random Quick Sort Count Averages\nMoves: " + quickMoveRand/5 + 
    	" Comparisons: " + quickCompRand/5);
    	System.out.println("Done!");
            
    }
}

