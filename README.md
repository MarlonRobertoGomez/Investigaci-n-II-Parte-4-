Adapter
// Interfaz existente
public interface IConexion {
    void Conectar();
}

// Clase existente
public class ConexionSQL : IConexion {
    public void Conectar() => Console.WriteLine("Conectado a SQL.");
}

// Nuevo sistema espera una nueva interfaz
public interface IConexionNoSQL {
    void ConectarNoSQL();
}

// Adaptador
public class ConexionAdapter : IConexionNoSQL {
    private readonly IConexion _conexion;

    public ConexionAdapter(IConexion conexion) {
        _conexion = conexion;
    }

    public void ConectarNoSQL() {
        _conexion.Conectar();
        Console.WriteLine("Adaptando conexión a NoSQL.");
    }
}

// Uso
class Program {
    static void Main() {
        IConexion conexionSQL = new ConexionSQL();
        IConexionNoSQL adaptador = new ConexionAdapter(conexionSQL);
        adaptador.ConectarNoSQL();
    }
}

Decorator
public interface ICafe {
    string ObtenerDescripcion();
    double ObtenerCosto();
}

public class CafeSimple : ICafe {
    public string ObtenerDescripcion() => "Café simple";
    public double ObtenerCosto() => 5.0;
}

// Decorador base
public abstract class CafeDecorador : ICafe {
    protected ICafe _cafe;

    public CafeDecorador(ICafe cafe) {
        _cafe = cafe;
    }

    public virtual string ObtenerDescripcion() => _cafe.ObtenerDescripcion();
    public virtual double ObtenerCosto() => _cafe.ObtenerCosto();
}

// Decoradores concretos
public class ConLeche : CafeDecorador {
    public ConLeche(ICafe cafe) : base(cafe) { }
    public override string ObtenerDescripcion() => _cafe.ObtenerDescripcion() + ", con leche";
    public override double ObtenerCosto() => _cafe.ObtenerCosto() + 2.0;
}

// Uso
class Program {
    static void Main() {
        ICafe cafe = new CafeSimple();
        Console.WriteLine($"{cafe.ObtenerDescripcion()} cuesta {cafe.ObtenerCosto()}");

        cafe = new ConLeche(cafe);
        Console.WriteLine($"{cafe.ObtenerDescripcion()} cuesta {cafe.ObtenerCosto()}");
    }
}

