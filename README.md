## EX. NO:2 IMPLEMENTATION OF PLAYFAIR CIPHER

 

## AIM:
 

 

To write a C program to implement the Playfair Substitution technique.

## DESCRIPTION:

The Playfair cipher starts with creating a key table. The key table is a 5×5 grid of letters that will act as the key for encrypting your plaintext. Each of the 25 letters must be unique and one letter of the alphabet is omitted from the table (as there are 25 spots and 26 letters in the alphabet).

To encrypt a message, one would break the message into digrams (groups of 2 letters) such that, for example, "HelloWorld" becomes "HE LL OW OR LD", and map them out on the key table. The two letters of the diagram are considered as the opposite corners of a rectangle in the key table. Note the relative position of the corners of this rectangle. Then apply the following 4 rules, in order, to each pair of letters in the plaintext:
1.	If both letters are the same (or only one letter is left), add an "X" after the first letter
2.	If the letters appear on the same row of your table, replace them with the letters to their immediate right respectively
3.	If the letters appear on the same column of your table, replace them with the letters immediately below respectively
4.	If the letters are not on the same row or column, replace them with the letters on the same row respectively but at the other pair of corners of the rectangle defined by the original pair.
## EXAMPLE:
![image](https://github.com/Hemamanigandan/EX-NO-2-/assets/149653568/e6858d4f-b122-42ba-acdb-db18ec2e9675)

 

## ALGORITHM:

STEP-1: Read the plain text from the user.

STEP-2: Read the keyword from the user.

STEP-3: Arrange the keyword without duplicates in a 5*5 matrix in the row order and fill the remaining cells with missed out letters in alphabetical order. Note that ‘i’ and ‘j’ takes the same cell.

STEP-4: Group the plain text in pairs and match the corresponding corner letters by forming a rectangular grid.

STEP-5: Display the obtained cipher text.

Nmae: Muthulakshmi D
Reg: 212223040122

Program:

```
def prepare_text(text):
    text = text.lower().replace(" ", "").replace("j", "i")
    new_text = ""
    i = 0

    while i < len(text):
        new_text += text[i]
        if i + 1 < len(text) and text[i] == text[i + 1]:
            new_text += 'x'  
        elif i + 1 < len(text):
            new_text += text[i + 1]
            i += 1
        i += 1

    if len(new_text) % 2 != 0:
        new_text += 'z'  

    return new_text

def generate_key_table(key):
    key = key.lower().replace(" ", "").replace("j", "i")
    key_square = ""

    for ch in key + "abcdefghiklmnopqrstuvwxyz":
        if ch not in key_square:
            key_square += ch

    table = [[key_square[i * 5 + j] for j in range(5)] for i in range(5)]
    return table

def find_position(table, letter):
    for i in range(5):
        for j in range(5):
            if table[i][j] == letter:
                return i, j
    return None

def encrypt(plain_text, key_table):
    cipher_text = ""
    plain_text = prepare_text(plain_text)

    for i in range(0, len(plain_text), 2):
        a, b = plain_text[i], plain_text[i + 1]
        row1, col1 = find_position(key_table, a)
        row2, col2 = find_position(key_table, b)

        if row1 == row2:  
            cipher_text += key_table[row1][(col1 + 1) % 5]
            cipher_text += key_table[row2][(col2 + 1) % 5]
        elif col1 == col2:  
            cipher_text += key_table[(row1 + 1) % 5][col1]
            cipher_text += key_table[(row2 + 1) % 5][col2]
        else:  
            cipher_text += key_table[row1][col2]
            cipher_text += key_table[row2][col1]

    return cipher_text

def decrypt(cipher_text, key_table):
    plain_text = ""

    for i in range(0, len(cipher_text), 2):
        a, b = cipher_text[i], cipher_text[i + 1]
        row1, col1 = find_position(key_table, a)
        row2, col2 = find_position(key_table, b)

        if row1 == row2:  
            plain_text += key_table[row1][(col1 - 1) % 5]
            plain_text += key_table[row2][(col2 - 1) % 5]
        elif col1 == col2:  
            plain_text += key_table[(row1 - 1) % 5][col1]
            plain_text += key_table[(row2 - 1) % 5][col2]
        else:  
            plain_text += key_table[row1][col2]
            plain_text += key_table[row2][col1]

    return plain_text

# input
print("PlayFair Cipher\n")
key = input("Enter the key: ")
plain_text = input("\nEnter the plaintext: ")

key_table = generate_key_table(key)
cipher_text = encrypt(plain_text, key_table)
decrypted_text = decrypt(cipher_text, key_table)

print("\nCipher Text:", cipher_text)
print("\nDecrypted Text:", decrypted_text)
```
## Output:

![424296846-c43b20a3-5bab-40e9-aec4-b3cbdccfd159](https://github.com/user-attachments/assets/5d68bc08-06c7-4922-8e07-fc16c1d756bb)


## Result :
   The program is executed successfully
