# project-password-generator
proyectos con python
import random
import string

def generar_contraseña(longitud):
    if longitud > 15:
        print("⚠️ Longitud máxima permitida es 15. Usando 15 caracteres.")
        longitud = 15

    if longitud < 4:
        print("⚠️ Se requieren al menos 4 caracteres para incluir todos los tipos.")
        longitud = 4

    mayuscula = random.choice(string.ascii_uppercase)
    minuscula = random.choice(string.ascii_lowercase)
    numero = random.choice(string.digits)
    simbolo = random.choice(string.punctuation)

    base = string.ascii_letters + string.digits + string.punctuation

    # Evitar repeticiones incluyendo los primeros 4 y luego el resto sin duplicar
    restantes = longitud - 4
    otros = random.sample(base.replace(mayuscula, "").replace(minuscula, "").replace(numero, "").replace(simbolo, ""), restantes)

    caracteres_finales = [mayuscula, minuscula, numero, simbolo] + otros
    random.shuffle(caracteres_finales)
    contraseña = ''.join(caracteres_finales)

    return contraseña

# 🎛️ Interfaz
print("🔐 Generador de Contraseñas Avanzado")
try:
    longitud = int(input("📏 Ingresa la longitud deseada (máx 15): "))
    contraseña_segura = generar_contraseña(longitud)

    print(f"\n🔓 Tu contraseña generada es:\n{contraseña_segura}")

    # 📝 Guardar en archivo
    with open("contraseña_generada.txt", "w") as archivo:
        archivo.write(contraseña_segura)
        print("💾 Contraseña guardada en 'contraseña_generada.txt'")

except ValueError:
    print("❌ Por favor ingresa un número válido.")
