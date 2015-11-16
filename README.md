# Proyecto1.0
package ecg;

import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.io.File;

import javax.swing.JButton;
import javax.swing.JFileChooser;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JMenu;
import javax.swing.JMenuBar;
import javax.swing.JMenuItem;
import javax.swing.JPanel;
import javax.swing.JTextArea;
import javax.swing.SwingUtilities;
import javax.swing.filechooser.FileNameExtensionFilter;

import giovynet.serial.Baud;
import giovynet.serial.Com;
import giovynet.serial.Parameters;

public class barras extends JFrame{
	public static String url;
	private JMenuBar barra1;
    private JMenu menu1,menu2;
    private JMenuItem item1, item2, item3, item4;
    private JFrame panel;
    private JButton b,b2;
	//JMenu barra;
private	JLabel title;
//	JLabel Menu;
	//JButton circuito;
private	JTextArea area;
	//JButton informacion;
	private JPanel j,x,k;
	 public barras(){

		 
		 
		 setLayout(null);
		 JPanel u=new JPanel();
		 u.setBounds(700, 600, 500, 100);
		  JPanel j= new JPanel();
		   j.setBounds(20, 50, 700, 500);
		  JPanel x= new JPanel();
		  x.setBounds(20, 50, 700, 500);
		  JPanel k= new JPanel();
		  k.setBounds(20, 50, 700, 500);
		  
		  title= new JLabel("Registro y Analisis de electrocardiograma");
		  title.setBounds(550, 1, 560, 30);

		  area=new JTextArea();
		  area.setBounds(40,600,600,50);
		  
		  
			panel= new JFrame();
			panel.setLayout(null);
			panel.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		    panel.setSize(1400,700);
		    panel.setVisible(true);
			panel.setExtendedState(JFrame.MAXIMIZED_BOTH);
			
			
				
			
			
			
		   barra1 = new JMenuBar();
		   setJMenuBar(barra1);
		   barra1.setVisible(true);
		   barra1.setBounds(1, 30, 1400, 30);
		   menu1 = new JMenu("Ayuda");
		   menu1.setBounds(50, 40, 50, 30);
		   menu1.setVisible(true);
		   menu2 = new JMenu("¿Como usar?");
		   menu2.setBounds(2, 40, 50, 30);
		   menu2.setVisible(true);
		   barra1.add(menu2);
		   barra1.add(menu1);
		   panel.add(area);
		   panel.add(title);
		   panel.add(barra1);
		   JButton b2=new JButton("Parar");
			 b2.setBounds(900, 600, 200, 100);
		   JButton b=new JButton("Iniciar");
		  b.setBounds(600, 600, 200, 100);
		  b.setVisible(true);
		  b.setLayout(null);
		  u.add(b);
		  u.add(b2);
		  panel.add(u);
	        b.addActionListener(new ActionListener() {
	        	 public void actionPerformed(ActionEvent l) {
		                ActionEvent va=l;
		               
		                try {
							Parameters settings = new Parameters();
						    settings.setPort("COM3");
						    settings.setBaudRate(Baud._9600);
						    settings.setMinDelayWrite(10);
						    Com com1 = new Com(settings);
						    for(int i = 1, j = 0; j < 100000; j++) {
						    	int t= 0;
						    			t=t+1;
							String entradaCom = com1.receiveSingleString();
							System.out.print(entradaCom);
						    }
						} catch (Exception e) {
						e.printStackTrace();
						}
		                
				
						
						
		                  
							
		        		
		        		   
		        			
		                 
						
		             }
		         });
			
	        b2.addActionListener(new ActionListener() {
	        	 public void actionPerformed(ActionEvent l) {
		                ActionEvent va=l;
		              
	        	 }
	        	 });
		  item1 = new JMenuItem("¿ECG?");  
		  item1.addActionListener(new ActionListener() {
		             @Override
		             
		             public void actionPerformed(ActionEvent e) {
		                ActionEvent va=e;
		               
						if (va== e) {
		                  panel.remove(x);
		                  panel.remove(k);
						
		                  
							// JFrame  l =new JFrame();
		                   //l.setLayout(null);
		        			
		        		  //  l.setSize(728, 546);
		        		   // l.setVisible(true);
		        			url="/imagen/im3.jpg";
		        		    imagen Imagen = new imagen(url);
		        		   j.add(Imagen);
		        		    panel.add(j);
		        		    panel.repaint();  
		        		
		        		   
		        			
		                 }
						
		             }
		         });
		         
		       menu1.add(item1);
		       item2 = new JMenuItem("¿Como se registra?");
		       item2.addActionListener(new ActionListener() {
		             @Override
		             public void actionPerformed(ActionEvent f) {
		                ActionEvent va=f;
		               panel.remove(j);
		               panel.remove(k);
						if (va== f) {
							
							
		                 //  JFrame  l =new JFrame();
		                 //   l.setLayout(null);
		        		//	l.setSize(638,499);
		        		//    l.setVisible(true);
		        		   url="/imagen/im4.jpg";
		        		   Img Im = new Img(url);
		        		 		  
						   x.add(Im);
						   panel.add(x);
		        		   
						   panel.repaint();  
		        			
		        			
		        			
		                 }
						 

		             }
		         });
		         menu1.add(item2);
		         item3 = new JMenuItem("¿Derivaciones?");	       
		         item3.addActionListener(new ActionListener() {
		             @Override
		             public void actionPerformed(ActionEvent o) {
		                ActionEvent va=o;
		               panel.remove(j);
		               panel.remove(x);
						if (va== o) {
							
							
		                 //  JFrame  l =new JFrame();
		                 //   l.setLayout(null);
		        		//	l.setSize(638,499);
		        		//    l.setVisible(true);
		        		   url="/imagen/im2.jpg";
		        		  imag im02 = new imag(url);
		        		 		  
						   k.add(im02);
						   panel.add(k);
		        		   
						   panel.repaint();  
		        			
		        			
		        			
		                 }
						 

		             }
		         });
		         menu1.add(item3);
		       
		     
	 }
	 public void actualizarPantalla(){ 
		 SwingUtilities.updateComponentTreeUI(this); 
		 this.validateTree(); }
		 
	 public static void main(String[] args) {
		    barras p = new barras();
		    
		   
		   

			
			
			}
}
