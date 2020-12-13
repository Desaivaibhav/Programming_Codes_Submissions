#(20, 20, 20), (20, 14, 5), (18, 8, 18)

I built the below algorithm in python which didnt ran fully due to Memory and CPU constraints, But above isthe submission of one of the good combinations for range (1,20) of 9 elemenets:

Main seperate tasks/process/Functions:
	a. identify elemenets:In the matrix(3x3) find elements which are multiple of sum of outcomes of 2 		rolled dices and note their positions. Pick one of the position randomly and mark it bold.
	b.Check for BINGO in 3x3 matrix see if any of the row has all elemenets marked / any of the column has 		all elements marked/ any of the 2 diagonal has all elements marked.

1.Take numbers 1 to 20 in a list 
2. Produce all combinations product which are of size 9 as list.
3. Starts a loop:For each combination is converted to dataframe(matrix 3 X 3) we play games(consists of turns) 50 times for each combiation
	i. Dice rolling turns is started (max 10000): two dices rolled their sum is taken and the sum and mtrix is passed to process :identify elemenets. The marked element is replaced with number 23(the first prime number after 20)
	ii. Check for Bingo is called after above event to see if BINGO occured.
	iii. if it did then the list is stored in dictionary along with a number which represents number of turns it took to reach a Bingo state.
	iv. The 50 times(games) are played to see the average of turns being taken to reach BINGO for the particular list.