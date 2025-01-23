# B2--Trabajo Consulta 2: Conexión base de datos relacional

## ¿Qué es JDBC y cuáles son sus componentes?

Java Database Connectivity (JDBC) es una API que permite a las aplicaciones Java interactuar con bases de datos relacionales utilizando SQL. Esta API proporciona un conjunto de interfaces y clases que estandarizan la forma en que las aplicaciones Java se conectan, consultan y manipulan datos en bases de datos. Los **componentes principales** de JDBC incluyen:

- **Driver JDBC**: Controladores específicos para cada sistema de gestión de bases de datos, que actúan como intermediarios entre la aplicación Java y la base de datos.
- **URL de conexión**: Cadena que identifica la base de datos a la que se desea acceder, incluyendo detalles como el tipo de base de datos, dirección del servidor y puerto.
- **API JDBC**: Conjuntos de interfaces en los paquetes `java.sql` y `javax.sql`, que permiten realizar operaciones como establecer conexiones, ejecutar consultas SQL y procesar resultados.

## Librerías de Scala para conectarse a bases de datos relacionales

A continuación se presentan dos librerías populares en Scala para conectarse a bases de datos relacionales:

| Librería         | Descripción                                                                 | Soporte de Transacciones | Compatibilidad con JDBC |
|------------------|-----------------------------------------------------------------------------|--------------------------|--------------------------|
| **Slick**        | Slick es un marco funcional para trabajar con bases de datos relacionales en Scala. Permite consultas SQL tipo DSL y es adecuado para proyectos que buscan un enfoque más funcional. | Sí                       | Total                    |
| **Doobie**       | Doobie es una librería funcional que permite la interacción con bases de datos usando un enfoque puro y seguro. Se basa en el uso de monadas para manejar efectos secundarios. | Sí                       | Total                    |

## Establecer una conexión a MySQL

### 1. Generar una base de datos en MySQL

Para crear una base de datos llamada `test_db`, puedes usar el siguiente comando SQL:


### 2. Generar una tabla con datos de prueba

A continuación, crea una tabla llamada `users` dentro de `test_db`:

# JDBC y Conexión a Bases de Datos en Scala

Java Database Connectivity (JDBC) es una API que permite a las aplicaciones Java interactuar con bases de datos relacionales utilizando SQL. Esta API proporciona un conjunto de interfaces y clases que estandarizan la forma en que las aplicaciones Java se conectan, consultan y manipulan datos en bases de datos. Los componentes principales de JDBC incluyen: **Driver JDBC**: Controladores específicos para cada sistema de gestión de bases de datos, que actúan como intermediarios entre la aplicación Java y la base de datos, **URL de Conexión**: Cadena que identifica la base de datos a la que se desea acceder, incluyendo detalles como el tipo de base de datos, dirección del servidor y puerto, **API JDBC**: Conjuntos de interfaces en los paquetes `java.sql` y `javax.sql`, que permiten realizar operaciones como establecer conexiones, ejecutar consultas SQL y procesar resultados.

A continuación se presentan dos librerías populares en Scala para conectarse a bases de datos relacionales: **Slick** es un marco funcional para trabajar con bases de datos relacionales en Scala. Permite consultas SQL tipo DSL y es adecuado para proyectos que buscan un enfoque más funcional. Soporta transacciones y tiene compatibilidad total con JDBC. **Doobie** es una librería funcional que permite la interacción con bases de datos usando un enfoque puro y seguro. Se basa en el uso de mónadas para manejar efectos secundarios. También soporta transacciones y es totalmente compatible con JDBC.

# SQL
![SQL](https://github.com/user-attachments/assets/e579150e-4c10-4539-90a6-f0748a16d495)

# SCALA
``` scala
import java.sql.{Connection, DriverManager, ResultSet}

object MySQLQuery {
  def main(args: Array[String]): Unit = {
    val url = "jdbc:mysql://localhost:3306/test_db1"
    val username = "root"
    val password = "utpl"

    var connection: Connection = null

    try {
      connection = DriverManager.getConnection(url, username, password)
      val statement = connection.createStatement()
      val resultSet: ResultSet = statement.executeQuery("SELECT * FROM estudiantes")

      while (resultSet.next()) {
        println(s"ID: ${resultSet.getInt("cedula")}, Name: ${resultSet.getString("nombre")}, Email: ${resultSet.getString("edad")}")
      }
    } catch {
      case e: Exception => e.printStackTrace()
    } finally {
      if (connection != null) {
        connection.close()
      }
    }
  }
}
```
![Scala](https://github.com/user-attachments/assets/99f447a0-68b9-42fa-8764-55a1167ee3a2)


