from itertools import *
import random


Empty = '-'
player1 = 'X'
computerAi = 'O'




def diagonalsrigth (matrix, cols, rows):                                                                  
        for di in ([(j, i - j) for j in range(cols)] for i in range( cols + rows -1) ):                   
                yield [matrix[i][j] for i, j in di if i >= 0 and j >= 0 and i < cols and j < rows]        
                                                                                                         



def diagonalsleft (matrix, cols, rows):                                                                   
        for di in ([(j, i - cols + j + 1) for j in range(cols)] for i in range( cols + rows - 1 )):       
                yield [matrix[i][j] for i, j in di if i >= 0 and j >= 0 and i < cols and j < rows]         
                                                                                                          


class connect4:
        def __init__ (self, cols = 7, rows = 6):        # Constractor
                self.cols = cols
                self.rows = rows
                self.board = [[Empty] * rows for i in range(cols)]  

        def INPUT_COIN (self, column, XO):
                c = self.board[column]
                if c[0] != Empty:
                        raise Exception('Column is full')

                i = -1
                while c[i] != Empty:
                        i -= 1
                c[i] = XO

                w = self.theWinner()
                if w:
                        self.GAME_GUI()
                        raise Exception(w + ' WIN :)' )


        def theWinner (self):
                lines = (
                        self.board,       # columns 
                        zip(*self.board),           # rows
                        diagonalsrigth(self.board, self.cols, self.rows),    # TOP RIGHT diagonals
                        diagonalsleft(self.board, self.cols, self.rows)      # TOP LEFT diagonals
                )

                for line in chain(*lines):
                        for XO, group in groupby(line):
                                if XO != Empty and len(list(group)) >= 4:
                                        return XO


        def GAME_GUI (self):
                print("0  1  2  3  4  5  6")
                for y in range(self.rows):
                        print('  '.join(str(self.board[x][y]) for x in range(self.cols)))
                



if __name__ == '__main__':
        C = connect4()                    # make a object of class connect4
        turn = player1
        while True:
                C.GAME_GUI()
               
                
                if turn == player1 :
                         column = input('{}\'s turn: '.format('player1' if turn == player1 else 'computerAi'))
                         X= C.INPUT_COIN(int(column),turn) 
                         turn = computerAi if turn == player1 else player1
                else :
                 
                  C.INPUT_COIN( random.randint(0, 6),turn)
                  turn = computerAi if turn == player1 else player1













