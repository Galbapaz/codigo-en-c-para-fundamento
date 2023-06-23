# codigo-en-cshare-para-fundamento
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        string usuario;
        string contrasena;

        // Registro de usuarios
        string duenoUsuario = "dueno";
        string duenoContrasena = "123456";
        string guardiaUsuario = "guardia";
        string guardiaContrasena = "abcdef";
        string gerenteUsuario = "gerente";
        string gerenteContrasena = "qwerty";

        // Autenticacion de usuarios
        Console.WriteLine("Inicio de Sesion");

        // Validacion de datos faltantes
        do
        {
            Console.Write("Usuario: ");
            usuario = Console.ReadLine();
            if (usuario == "")
            {
                Console.WriteLine("Debe ingresar un usuario. Intentelo nuevamente.");
            }
        } while (usuario == "");

        do
        {
            Console.Write("Contrasena: ");
            contrasena = Console.ReadLine();
            if (contrasena == "")
            {
                Console.WriteLine("Debe ingresar una contrasena. Intentelo nuevamente.");
            }
        } while (contrasena == "");

        Console.WriteLine();

        // Verificacion de credenciales
        if (usuario == duenoUsuario && contrasena == duenoContrasena)
        {
            Console.WriteLine("Bienvenido, dueno del edificio.");
        }
        else if (usuario == guardiaUsuario && contrasena == guardiaContrasena)
        {
            Console.WriteLine("Bienvenido, guardia de seguridad.");
        }
        else if (usuario == gerenteUsuario && contrasena == gerenteContrasena)
        {
            Console.WriteLine("Bienvenido, gerente.");
        }
        else
        {
            Console.WriteLine("Credenciales invalidas. Acceso denegado.");
            return;
        }

        // Verificacion de la hora actual
        DateTime now = DateTime.Now;
        int hora = now.Hour;
        int minuto = now.Minute;

        bool activarCamaras = false;

        // Verificar si es hora de activar las camaras
        if (hora > 22 || (hora == 22 && minuto >= 30) || hora < 6 || (hora == 6 && minuto <= 30))
        {
            activarCamaras = true;
        }

        const int numCamaras = 16;
        string[] estadoCamaras = new string[numCamaras];

        // Estado inicial de las camaras
        for (int i = 0; i < numCamaras; i++)
        {
            estadoCamaras[i] = activarCamaras ? "activada" : "desactivada";
        }

        // Verificar si es hora de activar los sensores de movimiento
        bool activarSensores = false;

        if (hora > 22 || (hora == 22 && minuto >= 30) || hora < 6 || (hora == 6 && minuto <= 30))
        {
            activarSensores = true;
        }

        const int numSensores = 16;
        bool[] estadoSensores = new bool[numSensores];

        // Estado inicial de los sensores de movimiento
        for (int i = 0; i < numSensores; i++)
        {
            estadoSensores[i] = activarSensores;
        }

        // Menu de opciones
        int opcion;
        do
        {
            Console.WriteLine();
            Console.WriteLine("Menu de opciones");
            Console.WriteLine("1. Ver estado de las camaras");
            Console.WriteLine("2. Activar todas las camaras");
            Console.WriteLine("3. Desactivar todas las camaras");
            Console.WriteLine("4. Ver estado de los sensores de movimiento");
            Console.WriteLine("5. Activar todos los sensores de movimiento");
            Console.WriteLine("6. Desactivar todos los sensores de movimiento");
            Console.WriteLine("7. Activar un sensor de movimiento");
            Console.WriteLine("8. Desactivar un sensor de movimiento");
            Console.WriteLine("9. Salir");
            Console.Write("Ingrese una opcion: ");
            opcion = Convert.ToInt32(Console.ReadLine());

            switch (opcion)
            {
                case 1:
                    Console.WriteLine("Estado de las camaras:");
                    for (int i = 0; i < numCamaras; i++)
                    {
                        Console.WriteLine("Camara " + (i + 1) + ": " + estadoCamaras[i]);
                    }
                    break;

                case 2:
                    for (int i = 0; i < numCamaras; i++)
                    {
                        estadoCamaras[i] = "activada";
                    }
                    Console.WriteLine("Todas las camaras han sido activadas correctamente.");
                    break;

                case 3:
                    for (int i = 0; i < numCamaras; i++)
                    {
                        estadoCamaras[i] = "desactivada";
                    }
                    Console.WriteLine("Todas las camaras han sido desactivadas correctamente.");
                    break;

                case 4:
                    Console.WriteLine("Estado de los sensores de movimiento:");
                    for (int i = 0; i < numSensores; i++)
                    {
                        Console.WriteLine("Sensor " + (i + 1) + ": " + (estadoSensores[i] ? "activado" : "desactivado"));
                    }
                    break;

                case 5:
                    for (int i = 0; i < numSensores; i++)
                    {
                        estadoSensores[i] = true;
                    }
                    Console.WriteLine("Todos los sensores de movimiento han sido activados correctamente.");
                    break;

                case 6:
                    for (int i = 0; i < numSensores; i++)
                    {
                        estadoSensores[i] = false;
                    }
                    Console.WriteLine("Todos los sensores de movimiento han sido desactivados correctamente.");
                    break;

                case 7:
                    int sensor;
                    Console.Write("Ingrese el numero de sensor a activar (1-" + numSensores + "): ");
                    sensor = Convert.ToInt32(Console.ReadLine());

                    if (sensor >= 1 && sensor <= numSensores)
                    {
                        estadoSensores[sensor - 1] = true;
                        Console.WriteLine("Sensor " + sensor + " activado correctamente.");
                    }
                    else
                    {
                        Console.WriteLine("Numero de sensor invalido.");
                    }
                    break;

                case 8:
                    int sensor2;
                    Console.Write("Ingrese el numero de sensor a desactivar (1-" + numSensores + "): ");
                    sensor2 = Convert.ToInt32(Console.ReadLine());

                    if (sensor2 >= 1 && sensor2 <= numSensores)
                    {
                        estadoSensores[sensor2 - 1] = false;
                        Console.WriteLine("Sensor " + sensor2 + " desactivado correctamente.");
                    }
                    else
                    {
                        Console.WriteLine("Numero de sensor invalido.");
                    }
                    break;

                case 9:
                    Console.WriteLine("Saliendo del programa...");
                    break;

                default:
                    Console.WriteLine("Opcion invalida. Por favor, ingrese una opcion valida.");
                    break;
            }
        } while (opcion != 9);
    }
}
