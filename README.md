# codigo-en-c-para-fundamento
using System;

namespace SistemaSeguridad
{
    class Program
    {
        static void Main(string[] args)
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

            // Autenticación de usuarios
            Console.WriteLine("Inicio de Sesión");
            Console.Write("Usuario: ");
            usuario = Console.ReadLine();
            Console.Write("Contraseña: ");
            contrasena = Console.ReadLine();
            Console.WriteLine();

            // Verificación de credenciales
            if (usuario == duenoUsuario && contrasena == duenoContrasena)
            {
                Console.WriteLine("Bienvenido, dueño del edificio.");
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
                Console.WriteLine("Credenciales inválidas. Acceso denegado.");
                return;
            }

            // Verificación de la hora actual
            DateTime tiempoActual = DateTime.Now;
            int hora = tiempoActual.Hour;
            int minuto = tiempoActual.Minute;

            bool activarCamaras = false;

            // Verificar si es hora de activar las cámaras
            if (hora > 22 || (hora == 22 && minuto >= 30) || hora < 6 || (hora == 6 && minuto <= 30))
            {
                activarCamaras = true;
            }

            const int numCamaras = 16;
            string[] estadoCamaras = new string[numCamaras];

            // Estado inicial de las cámaras
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

            // Menú de opciones
            int opcion;
            do
            {
                Console.WriteLine();
                Console.WriteLine("Menú de opciones");
                Console.WriteLine("1. Ver estado de las cámaras");
                Console.WriteLine("2. Activar todas las cámaras");
                Console.WriteLine("3. Desactivar todas las cámaras");
                Console.WriteLine("4. Ver estado de los sensores de movimiento");
                Console.WriteLine("5. Activar todos los sensores de movimiento");
                Console.WriteLine("6. Desactivar todos los sensores de movimiento");
                Console.WriteLine("7. Activar una cámara");
                Console.WriteLine("8. Desactivar una cámara");
                Console.WriteLine("9. Activar un sensor de movimiento");
                Console.WriteLine("10. Desactivar un sensor de movimiento");
                Console.WriteLine("11. Salir");
                Console.Write("Ingrese una opción: ");
                opcion = int.Parse(Console.ReadLine());

                switch (opcion)
                {
                    case 1:
                        Console.WriteLine("Estado de las cámaras:");
                        for (int i = 0; i < numCamaras; i++)
                        {
                            Console.WriteLine($"Cámara {i + 1}: {estadoCamaras[i]}");
                        }
                        break;
                    case 2:
                        for (int i = 0; i < numCamaras; i++)
                        {
                            estadoCamaras[i] = "activada";
                        }
                        Console.WriteLine("Todas las cámaras han sido activadas correctamente.");
                        break;
                    case 3:
                        for (int i = 0; i < numCamaras; i++)
                        {
                            estadoCamaras[i] = "desactivada";
                        }
                        Console.WriteLine("Todas las cámaras han sido desactivadas correctamente.");
                        break;
                    case 4:
                        Console.WriteLine("Estado de los sensores de movimiento:");
                        for (int i = 0; i < numSensores; i++)
                        {
                            Console.WriteLine($"Sensor {i + 1}: {(estadoSensores[i] ? "activado" : "desactivado")}");
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
                        int camara;
                        Console.Write("Ingrese el número de cámara a activar (1-" + numCamaras + "): ");
                        camara = int.Parse(Console.ReadLine());

                        if (camara >= 1 && camara <= numCamaras)
                        {
                            estadoCamaras[camara - 1] = "activada";
                            Console.WriteLine("Cámara " + camara + " activada correctamente.");
                        }
                        else
                        {
                            Console.WriteLine("Número de cámara inválido.");
                        }
                        break;
                    case 8:
                        Console.Write("Ingrese el número de cámara a desactivar (1-" + numCamaras + "): ");
                        camara = int.Parse(Console.ReadLine());

                        if (camara >= 1 && camara <= numCamaras)
                        {
                            estadoCamaras[camara - 1] = "desactivada";
                            Console.WriteLine("Cámara " + camara + " desactivada correctamente.");
                        }
                        else
                        {
                            Console.WriteLine("Número de cámara inválido.");
                        }
                        break;
                    case 9:
                        int sensor;
                        Console.Write("Ingrese el número de sensor a activar (1-" + numSensores + "): ");
                        sensor = int.Parse(Console.ReadLine());

                        if (sensor >= 1 && sensor <= numSensores)
                        {
                            estadoSensores[sensor - 1] = true;
                            Console.WriteLine("Sensor " + sensor + " activado correctamente.");
                        }
                        else
                        {
                            Console.WriteLine("Número de sensor inválido.");
                        }
                        break;
                    case 10:
                        Console.Write("Ingrese el número de sensor a desactivar (1-" + numSensores + "): ");
                        sensor = int.Parse(Console.ReadLine());

                        if (sensor >= 1 && sensor <= numSensores)
                        {
                            estadoSensores[sensor - 1] = false;
                            Console.WriteLine("Sensor " + sensor + " desactivado correctamente.");
                        }
                        else
                        {
                            Console.WriteLine("Número de sensor inválido.");
                        }
                        break;
                    case 11:
                        Console.WriteLine("Saliendo del programa...");
                        break;
                    default:
                        Console.WriteLine("Opción inválida. Por favor, ingrese una opción válida.");
                        break;
                }
            } while (opcion != 11);
        }
    }
}








