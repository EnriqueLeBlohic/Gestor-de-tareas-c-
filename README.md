# Gestor-de-tareas-c-
un gestor de tareas sencillo, agregar, modificar, eliminar, salir, etc
using System;
using System.Collections.Generic;

namespace GestorTareas
{
   class Program
   {
    static void Main(string[] args)
    {
        List<Tarea> listaTareas = new List<Tarea>();
        while (true)
        {
            Console.WriteLine("\nBienvenido al Gestor de Tareas");
            Console.WriteLine("Elija una opción");
            Console.WriteLine("1. Agregar tarea");
            Console.WriteLine("2. cambiar estado");
            Console.WriteLine("3. Ver tareas");
            Console.WriteLine("4. Modificar tarea");
            Console.WriteLine("5. Eliminar tarea");
            Console.WriteLine("6. Salir\n");

            int opcion = Convert.ToInt32(Console.ReadLine());

            switch (opcion)
            {
                case 1:
                    AgregarTarea(listaTareas);
                    break;
                case 2:
                    CambiarEstado(listaTareas);
                    break;
                case 3:
                    VerTareas(listaTareas);
                    break;
                case 4:
                    ModificarTarea(listaTareas);
                    break;
                case 5:
                    EliminarTarea(listaTareas);
                    break;
                case 6:
                    Console.WriteLine("Hasta Luego");
                    return;
                default:
                    Console.WriteLine("¡Opcion invalida!");
                    return;
            }

        }
    }
    static void AgregarTarea(List<Tarea> lista)
    {
        Console.WriteLine("Ingrese la descripción de la tarea: ");
        string descripción = Console.ReadLine();
        Console.WriteLine("¿La tarea está completada? (s/n): ");
        bool completada = Console.ReadLine().ToLower() == "s" ? true: false;

        Tarea nuevaTarea = new Tarea(descripción, completada);
        lista.Add(nuevaTarea);
        
        Console.WriteLine("Tarea Agregada correctamente. \n");

    }
    static void CambiarEstado(List<Tarea> lista)
    {
        VerTareas(lista);
        if (lista.Count == 0)
        {
            return;
        }
        Console.WriteLine("Ingrese el nímero de la tarea para cambiar el estado: ");
        int indice = Convert.ToInt32(Console.ReadLine()) - 1;

        if(indice >= 0 && indice <lista.Count)
        {
            Console.WriteLine("¿La tarea está completada? (s/n): ");
            bool nuevaCompletada = Console.ReadLine().ToLower() == "s" ? true: false;

            lista[indice].Completada = nuevaCompletada;

            Console.WriteLine("estado cambiado exitosamente. \n");
        }
        else
        {
            Console.WriteLine("Numero de tarea inválido. \n");
        }
    }

    static void VerTareas(List<Tarea> lista)
    {
        if (lista.Count == 0)
        {
            Console.WriteLine("No hay tareas a mostrar. \n");
        }
        else
        {
            Console.WriteLine("Lista de tarea: \n");
            for(int i=0; i < lista.Count; i++)
            {
                Console.WriteLine($"{i + 1}. {lista[i].Descripcion} - {(lista[i].Completada ? "Completada" : "Pendiente")}");
            }
        }
    }
    static void ModificarTarea(List<Tarea> lista)
    {
        VerTareas(lista);
        if (lista.Count == 0)
        {
            return;
        }
        Console.WriteLine("Ingrese el nímero de la tarea que deseas modificar: ");
        int indice = Convert.ToInt32(Console.ReadLine()) - 1;

        if(indice >= 0 && indice <lista.Count)
        {
            Console.WriteLine("Ingrese la nueva descripción de la tarea: ");
            string nuevaDescripcion = Console.ReadLine();
            Console.WriteLine("¿La tarea está completada? (s/n): ");
            bool nuevaCompletada = Console.ReadLine().ToLower() == "s" ? true: false;

            lista[indice].Descripcion = nuevaDescripcion;
            lista[indice].Completada = nuevaCompletada;

            Console.WriteLine("Tarea modificada exitosamente. \n");
        }
        else
        {
            Console.WriteLine("Numero de tarea inválido. \n");
        }
    }

    static void EliminarTarea(List<Tarea> lista)
    {
        VerTareas(lista);
        if (lista.Count == 0)
        {
            return;
        }
        Console.WriteLine("Ingrese el número de la tarea que desea eliminar: ");
        int indice = Convert.ToInt32(Console.ReadLine()) - 1;

        if (indice >=0 && indice < lista.Count)
        {
            lista.RemoveAt(indice);
            Console.WriteLine("Tarea eliminada exitosamente. \n");
        }
        else
        {
            Console.WriteLine("Número de tarea invalido. \n");
        }
    }

   }
   class Tarea
   {
      public string Descripcion {get; set;}
      public bool Completada {get; set;}

      public Tarea(string descripción, bool completada)
      {
        Descripcion = descripción;
        Completada = completada;
      }
   }
}
