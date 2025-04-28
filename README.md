# MorseCodeDecode
Code and decode using old Morse code


import tkinter as tk
from tkinter import messagebox

class MorseCodeConverter:
    def __init__(self, root):
        self.root = root
        self.root.title("Morse Code Converter")
        self.root.geometry("600x400")

        # Morse code dictionary
        self.morse_dict = {
            'A': '.-', 'B': '-...', 'C': '-.-.', 'D': '-..', 'E': '.',
            'F': '..-.', 'G': '--.', 'H': '....', 'I': '..', 'J': '.---',
            'K': '-.-', 'L': '.-..', 'M': '--', 'N': '-.', 'O': '---',
            'P': '.--.', 'Q': '--.-', 'R': '.-.', 'S': '...', 'T': '-',
            'U': '..-', 'V': '...-', 'W': '.--', 'X': '-..-', 'Y': '-.--',
            'Z': '--..', '0': '-----', '1': '.----', '2': '..---', '3': '...--',
            '4': '....-', '5': '.....', '6': '-....', '7': '--...', '8': '---..',
            '9': '----.', ' ': ' '
        }
        # Reverse dictionary for decoding
        self.reverse_morse = {value: key for key, value in self.morse_dict.items()}

        # GUI elements
        # Encode section
        self.label_encode = tk.Label(root, text="Enter Text to Encode to Morse Code:")
        self.label_encode.pack(pady=10)

        self.encode_input = tk.Text(root, height=2, width=50)
        self.encode_input.pack()

        self.encode_button = tk.Button(root, text="Encode to Morse", command=self.encode)
        self.encode_button.pack(pady=5)

        self.encode_output = tk.Text(root, height=2, width=50, state='disabled')
        self.encode_output.pack()

        # Decode section
        self.label_decode = tk.Label(root, text="Enter Morse Code to Decode to Text (use spaces between codes):")
        self.label_decode.pack(pady=20)

        self.decode_input = tk.Text(root, height=2, width=50)
        self.decode_input.pack()

        self.decode_button = tk.Button(root, text="Decode to Text", command=self.decode)
        self.decode_button.pack(pady=5)

        self.decode_output = tk.Text(root, height=2, width=50, state='disabled')
        self.decode_output.pack()

    def encode(self):
        text = self.encode_input.get("1.0", tk.END).strip().upper()
        result = []
        
        for char in text:
            if char in self.morse_dict:
                result.append(self.morse_dict[char])
            else:
                messagebox.showerror("Error", "Invalid character detected. Use letters, numbers, and spaces only.")
                return
        
        morse_code = ' '.join(result)
        
        # Update output
        self.encode_output.config(state='normal')
        self.encode_output.delete("1.0", tk.END)
        self.encode_output.insert(tk.END, morse_code)
        self.encode_output.config(state='disabled')

    def decode(self):
        morse = self.decode_input.get("1.0", tk.END).strip()
        morse_codes = morse.split()
        result = []
        
        for code in morse_codes:
            if code in self.reverse_morse:
                result.append(self.reverse_morse[code])
            else:
                messagebox.showerror("Error", "Invalid Morse code detected. Use valid Morse code symbols separated by spaces.")
                return
        
        text = ''.join(result)
        
        # Update output
        self.decode_output.config(state='normal')
        self.decode_output.delete("1.0", tk.END)
        self.decode_output.insert(tk.END, text)
        self.decode_output.config(state='disabled')

def main():
    root = tk.Tk()
    app = MorseCodeConverter(root)
    root.mainloop()

if __name__ == "__main__":
    main()
