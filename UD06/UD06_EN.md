---
title: UD06: Code documentation
language: EN
author: David Martínez Peña [www.martinezpenya.es]
subject: Development Environments
keywords: [EED, 2022, Environments, Development]
IES:IES Mestre Ramón Esteve (Catadau) [iesmre.es]
header: ${title} - ${subject} (ver: ${today})
footer: ${currentFileName}.pdf - ${author} - ${IES} - ${pageNo}/${pageCount}
typora-root-url: ${filename}/../
typora-copy-images-to: ${filename}/../assets
---
[toc]

# Introduction

Documenting a program's code is adding enough information to explain what it does, point by point, so that not only do computers know what to do, but humans also understand what they are doing and why.

Because between what a program has to do and how it does it there is an impressive distance: all the hours that the programmer has spent developing a solution and writing it in the corresponding language for the computer to run blindly.

Documenting a program is not only an act of good work of the programmer for that of leaving the work finished. It is also a need that is only appreciated in its due magnitude when there are errors to repair or the program must be extended with new capabilities or adapted to a new scenario. There are two rules that should never be forgotten:

1. all programs have errors and discovering them is only a matter of time and that the program succeeds and is used frequently 
2. all programs undergo modifications throughout their lives, at least all those that are successful

A program, if successful, will probably be modified in the future by the person who coded it or by another programmer. Thinking about this code review is why it is important that the program is understood: to be able to repair and modify it.

# What needs to be documented?

We must add explanations to everything that is not obvious.

Do not repeat what you do, but explain why it is done

And that translates into:

- What is a class in charge of? a package?
- what does a method do?
- what is the expected use of a method?
- What is a variable or attribute used for?
- what is the expected use of an attribute?
- what algorithm are we using? Where did we get it?
- what limitations does the algorithm have? What are the limitations of the implementation?
- what should be improved... if there was time?

# Types of comments

In Java we have three notations to introduce comments:

**One-line comments**:

- They start with the characters "//" and end with the line
- It is used to document code that we do not need to appear in the external documentation (the one generated by javadoc). these types of comments are used even when the comment takes up several lines, each of which begins with "//"

**Multi-line comments:**

- They begin with the characters "`/*`" and end with the characters "`*/`".
- Often used to remove code. It is common that obsolete code does not want it to disappear and we keep it "just in case". So that it does not run, it is commented.
  (In English it is usually called "comment out")

**Javadoc comments:**

- They begin with the characters "`/**`", can be extended along several lines (which probably begin with the character "*") and end with the characters "`*/`".
- They are used to generate external documentation.

# When should I put a comment?

1. Always, at the beginning of each class
2. Always, at the beginning of each method
3. Always, before each class variable (static attributes, constants).
4. At the beginning of a code snippet that is not obvious.
5. When the program does something "weird"

> Note: When a program is modified, the comments must be modified at the same time, other than
> that the comments end up referring to an algorithm that we no longer use.

# JavaDoc

The Java development package includes a tool, javadoc, to generate a set of web pages from the code files. This tool takes into consideration some feedback to generate a well-presented documentation of classes and class components (variables and methods).

Although javadoc does not help the understanding of the details of code, it does help the understanding of the architecture of the solution, which is not little. Javadoc is said to focus on the interface (API - Application Programming Interface) of Java classes and packages.

Javadoc highlights some comments, of which it requires a special syntax. They should start with "`/**`" and end with "`*/`", including a description and some special tags:

```java
/**
* Descriptive part.
* Which may consist of several sentences or paragraphs.
*
* @label specific label text
*/
```

These special comments must appear just before the declaration of a class, attribute, or method in the same source code. The following sections detail the tags that javadoc interprets and then converts into documentation.

As a general rule, it should be noted that the first sentence (the text up to the first point) will receive a prominent treatment, so it must provide a concise and forceful explanation of the documented element. The other sentences will go into detail.

| Label | Where to use | Objective |
| --------------------------------- | ---------------------------------------- | ------------------------------------------------------------ |
| `@autor` name | Classes, interfaces, | Indicate the author of the code. A label is put on each author |
| `@version` VersionIdentifier |Classes, interfaces, | Information about version |
| `@since` | Classes, methods | From which version it is. Ex: from JDK 1.1 |
| `@deprecated` | Classes, methods | To indicate that something should not be used anymore, it has become obsolete, even if it is maintained for compatibility. It is usually accompanied by what is to be used in your place. |
| `@see` ClassName | Classes, interfaces, methods, and attributes. | You will put the address to connect to this class in the documentation |
| `@see` ClassName#MethodName | Classes, interfaces, methods, and attributes. | You will put the address to connect with this method in the documentation. |
| `@return` description | Methods | To describe the values returned by each method and its type. |
| `@exception` name description | Methods | Exceptions that the method can raise. A label is put on each possible exception. They are usually sorted alphabetically. |
| `@param` name description | Methods | To describe the parameters, their use and their type. A label is put for each parameter |

# JavaDoc generation in NetBeans

Javadoc is a tool that processes documentation declarations and comments in a set of java source files. From that information it generates a set of html pages that describe the classes, methods, fields...

Here is an example of the documentation generated:

![Java 18 API](/assets/Screenshot_20220426_180214.png)

As you can see, the java documentation itself is created with the javadoc tool (the capture is the java API documentation). Some of the great advantages of this documentation is that:

- **it is navigable**: having a web format, you can click on the classes and navigate. In general it is more comfortable than a printed document because it avoids having to search pages
- **it is generated automatically**: it costs less to update, it does not generate formatting problems, it can be centralized...
- **it is very easy to create**: the programmer has to write, but with basically the same comments that he already adds to the code. The special javadoc language is very, very simple.

Most current IDEs have the API integrated into the help system of the environment, so while we write the code we are already shown related information:

![NetBeans JavaDoc](/assets/image-20220426181246718.png)

You could generate Javadoc right-clicking on your project and selecting `Generate Javadoc`:

![image-20220426182227709](/assets/generateJavaDoc.png)

This would create a structure folder inside your project folder `projectFolder\dist\javadoc\packageName\` with all the files needed to show documentation.

![folder](/assets/Screenshot_20220426_185229.png)

## Comment Editing

Comments written by the programmer are considered as text. However it is also optionally possible to write the comments using html internally. In this way we can create a presentation of the documentation more visual and comfortable. Obviously for this, the programmer must be familiar with the syntax of some basic html tags. 

On the comments, it is also important to note that the main purpose of the documentation is to make it useful. The documentation of an API is used to learn (or remember) what and how a set of classes work. Therefore, when documenting it is sought that the information is practical, we must tell what is important and the more summarized it is the better.

HTML comments:

```java
[...]
//Metodos privados
    /**
     * Comprueba que el nombre no este vacio
     * @return <ul>
     *  <li>true: el nombre es una cadena vacia</li>
     *  <li>false: el nombre no es una cadena vacia</li>
     *  </ul>
     */
    private boolean compruebaNombre(){
        if(nombre.equals("")){
            return false;
        }
        return true;
    }
[...]
```

Will be shown like this:

![HTML comments](/assets/Screenshot_20220426_181722.png)





# JavaDoc Sample

```java
/**
 * Clase Empleado
 *
 * Contiene informacion de cada empleado
 *
 * @author Fernando
 * @version 1.0
 */
public class Empleado {
 
    //Atributos
 
    /**
     * Nombre del empleado
     */
    private String nombre;
    /**
     * Apellido del empleado
     */
    private String apellido;
    /**
     * Edad del empleado
     */
    private int edad;
    /**
     * Salario del empleado
     */
    private double salario;
 
    //Metodos publicos
 
    /**
     * Suma un plus al salario del empleado si el empleado tiene mas de 40 años
     * @param sueldoPlus
     * @return <ul>
     *          <li>true: se suma el plus al sueldo</li>
     *          <li>false: no se suma el plus al sueldo</li>
     *          </ul>
     */
    public boolean plus (double sueldoPlus){
        boolean aumento=false;
        if (edad>40 && compruebaNombre()){
            salario+=sueldoPlus;
            aumento=true;
        }
        return aumento;
    }
 
    //Metodos privados
    /**
     * Comprueba que el nombre no este vacio
     * @return <ul>
     *  <li>true: el nombre es una cadena vacia</li>
     *  <li>false: el nombre no es una cadena vacia</li>
     *  </ul>
     */
    private boolean compruebaNombre(){
        if(nombre.equals("")){
            return false;
        }
        return true;
    }
 
    //Constructores
    /**
     * Constructor por defecto
     */
    public Empleado(){
        this ("", "", 0, 0);
    }
 
    /**
     * Constructor con 4 parametros
     * @param nombre nombre del empleado
     * @param apellido nombre del empleado
     * @param edad edad del empleado
     * @param salario salario del empleado
     */
    public Empleado(String nombre, String apellido, int edad, double salario){
        this.nombre=nombre;
        this.apellido=apellido;
        this.edad=edad;
        this.salario=salario;
    }
}
```

# Information sources

- [Wikipedia](https://es.wikipedia.org)
- [Uml Diagrams](https://www.uml-diagrams.org/)
- [Code&Coke (Fernando Valdeón)](http://entornos.codeandcoke.com/doku.php?id=start)
- Apuntes IES El Grao (Mª Isabel Barquilla?)
- [Apuntes IOC (Marcel García)](https://ioc.xtec.cat/materials/FP/Recursos/fp_dam_m05_/web/fp_dam_m05_htmlindex/index.html)
- [Apuntes José Luis Comesaña](https://www.sitiolibre.com/)
- [Apuntes IES Luis Vélez de Guevara 17-18 (José Antonio Muñoz Jiménez)](http://jamj2000.github.io/slides/2017/09/05/entornosdesarrollo/)

- Oracle provides material on how to document program interfaces: ([How to write doc comments for the javadoc tool](https://www.oracle.com/technical-resources/articles/java/javadoc-tool.html))