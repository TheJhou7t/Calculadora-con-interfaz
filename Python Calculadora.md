# "Calculadora-con-interfaz"
# "Jhouran Del Toro"

import tkinter as tk
from tkinter import messagebox
import math

# Funciones de la calculadora
def agregar_a_pantalla(valor):
    pantalla.insert(tk.END, valor)

def limpiar_pantalla():
    pantalla.delete(0, tk.END)

def calcular():
    try:
        expresion = pantalla.get()
        resultado = eval(expresion)
        limpiar_pantalla()
        pantalla.insert(0, str(resultado))
    except Exception as e:
        messagebox.showerror("Error", "Expresión inválida")

def calcular_funcion(func):
    try:
        expresion = pantalla.get()
        if func == "sin":
            resultado = math.sin(math.radians(float(expresion)))
        elif func == "cos":
            resultado = math.cos(math.radians(float(expresion)))
        elif func == "tan":
            resultado = math.tan(math.radians(float(expresion)))
        elif func == "log":
            resultado = math.log10(float(expresion))
        elif func == "ln":
            resultado = math.log(float(expresion))
        elif func == "sqrt":
            resultado = math.sqrt(float(expresion))
        elif func == "exp":
            resultado = math.exp(float(expresion))
        limpiar_pantalla()
        pantalla.insert(0, str(resultado))
    except Exception as e:
        messagebox.showerror("Error", "Operación inválida")

# Crear la ventana principal
ventana = tk.Tk()
ventana.title("Calculadora Científica")
ventana.geometry("400x600")
ventana.resizable(False, False)

# Pantalla de la calculadora
pantalla = tk.Entry(ventana, font=("Arial", 20), borderwidth=5, relief=tk.RIDGE, justify="right")
pantalla.grid(row=0, column=0, columnspan=4, padx=10, pady=10)

# Botones
botones = [
    ("7", 1, 0), ("8", 1, 1), ("9", 1, 2), ("/", 1, 3),
    ("4", 2, 0), ("5", 2, 1), ("6", 2, 2), ("*", 2, 3),
    ("1", 3, 0), ("2", 3, 1), ("3", 3, 2), ("-", 3, 3),
    ("0", 4, 0), (".", 4, 1), ("=", 4, 2), ("+", 4, 3),
]

for texto, fila, columna in botones:
    if texto == "=":
        boton = tk.Button(ventana, text=texto, font=("Arial", 15), bg="#4CAF50", fg="white",
                          command=calcular, height=2, width=5)
    else:
        boton = tk.Button(ventana, text=texto, font=("Arial", 15), command=lambda t=texto: agregar_a_pantalla(t),
                          height=2, width=5)
    boton.grid(row=fila, column=columna, padx=5, pady=5)

# Botones para funciones científicas
funciones = [
    ("sin", 5, 0), ("cos", 5, 1), ("tan", 5, 2), ("sqrt", 5, 3),
    ("log", 6, 0), ("ln", 6, 1), ("exp", 6, 2), ("C", 6, 3)
]

for texto, fila, columna in funciones:
    if texto == "C":
        boton = tk.Button(ventana, text=texto, font=("Arial", 15), bg="#f44336", fg="white",
                          command=limpiar_pantalla, height=2, width=5)
    else:
        boton = tk.Button(ventana, text=texto, font=("Arial", 15),
                          command=lambda f=texto: calcular_funcion(f), height=2, width=5)
    boton.grid(row=fila, column=columna, padx=5, pady=5)

# Iniciar la aplicación
ventana.mainloop()
