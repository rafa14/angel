angel
=====

angel/calculadora
package Calculadora;

import javax.swing.*; 

import java.awt.*; 
import java.awt.event.*; 

import javax.script.ScriptEngine; 
import javax.script.ScriptEngineManager; 
import javax.script.ScriptException; 

public class Calculadora extends JFrame implements ActionListener 
{ 
/**
	 * 
	 */
	private static final long serialVersionUID = 1L;
JPanel panel1= new JPanel(); 
JPanel panel2= new JPanel(); 

JTextField texto, campoTexto1, campoTexto2; 
String resultado; 
String formula=""; 
int a=0; 

public Calculadora() 
{ 
setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE); 

Container contenedor = getContentPane(); 

panel1.setLayout( new GridLayout(2,2) ); 

texto= new JTextField( "operacion" ); 
texto.setEditable( false ); 
panel1.add(texto); 

campoTexto1= new JTextField(10); 
campoTexto1.setEditable( false ); 
panel1.add( campoTexto1); 

texto= new JTextField( "Resultado" ); 
texto.setEditable(false); 
panel1.add(texto); 

campoTexto2= new JTextField(10); 
campoTexto2.setEditable( false ); 
panel1.add( campoTexto2); 


contenedor.add(panel1,"North" ); 

panel2.setLayout(new FlowLayout()); 

for(int i=0; i<10; i++) 
{ 
JButton boton= new JButton(""+i); 
boton.addActionListener(this); 
panel2.add(boton); 
} 

JButton botonSumar= new JButton("+" ); 
botonSumar.addActionListener(this); 
panel2.add(botonSumar); 

JButton botonRestar= new JButton("-" ); 
botonRestar.addActionListener(this); 
panel2.add(botonRestar); 

JButton botonMultiplicar= new JButton("*" ); 
botonMultiplicar.addActionListener(this); 
panel2.add(botonMultiplicar); 

JButton botonDividir= new JButton("/" ); 
botonDividir.addActionListener(this); 
panel2.add(botonDividir); 

JButton botonIgual= new JButton("=" ); 
botonIgual.addActionListener(this); 
panel2.add(botonIgual); 

JButton botonLimpiar = new JButton("Limpiar" ); 
botonLimpiar.addActionListener(this); 
panel2.add(botonLimpiar); 

contenedor.add(panel2,"Center" ); 

setSize(450, 140); 
setVisible(true); 
} 


public void actionPerformed(ActionEvent evento) 
{ 
ScriptEngineManager manager = new ScriptEngineManager(); 
ScriptEngine engine = manager.getEngineByName("js" ); 


if(a==1&&(!(evento.getActionCommand()).equals("=" ))) 
{ 
setResultado("" ); 
} 


if((evento.getActionCommand()).equals("Limpiar" )) 
{ 
setFormula("" ); 
setResultado("" ); 
formula=""; 
resultado=null; 
} 


if(!((evento.getActionCommand()).equals("=" )||(evento.getActionCommand()).equals("Limpiar" ))) 
{ 
formula=formula+evento.getActionCommand(); 
setFormula(formula); 
} 


if((evento.getActionCommand()).equals("=" )) 
{ 
try 
{ 
resultado= ""+engine.eval(formula); 

if(!(resultado.equals("null" ))) 
{ 
if(resultado.equals("Infinity" )||resultado.equals("NaN" )) 
{ 
setFormula(formula); 
setResultado("Math Error" ); 
} 
else 
{ 
setFormula(formula); 
setResultado(""+resultado); 
} 
} 

formula=""; 
} 
catch(ScriptException se) 
{ 
formula=""; 
setResultado("Syntax Error " ); 
} 
a=1; 
} 
} 


public void setFormula(String laFormula) 
{ 
campoTexto1.setText(laFormula); 
} 


public void setResultado(String elResultado) 
{ 
campoTexto2.setText(elResultado); 
} 


public static void main(String args[]) 
{ 
new Calculadora(); 
} 
}
