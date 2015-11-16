# Proyecto1.0
package proyecto2;
import gnu.io.CommPortIdentifier;
import gnu.io.PortInUseException;
import gnu.io.SerialPort;
import gnu.io.UnsupportedCommOperationException;
 
import java.awt.Color;
import java.awt.Graphics;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;
import java.util.Enumeration;
 
import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JPanel;
import javax.swing.JTextField;
import javax.swing.border.EmptyBorder;
public class Ventana extends JFrame {
 
    private JPanel contentPane;
    private JTextField textField;
    Enumeration puertos_libres =null;
    CommPortIdentifier port=null;
    SerialPort puerto_ser = null;
    OutputStream out = null;
    InputStream in = null;
    int VOLTAJE;
    Thread timer;
    JLabel lblNewLabel;
    JButton btnNewButton,btnNewButton_1;
    public Ventana() {
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setBounds(100, 100, 636, 365);
        contentPane = new JPanel();
        contentPane.setBorder(new EmptyBorder(5, 5, 5, 5));
        setContentPane(contentPane);
        contentPane.setLayout(null);
         timer = new Thread(new ImplementoRunnable());
         timer.start();
         timer.interrupt();
        btnNewButton = new JButton("Conectar");
        btnNewButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                  puertos_libres = CommPortIdentifier.getPortIdentifiers();
                    int aux=0;
                    while (puertos_libres.hasMoreElements())
                    {
                     port = (CommPortIdentifier) puertos_libres.nextElement();
                     int type = port.getPortType();
                     if (port.getName().equals(textField.getText()))
                     {
                            try {
                                puerto_ser = (SerialPort) port.open("puerto serial", 2000);
                                   int baudRate = 9600; // 9600bps
                                   //configuracion de arduino
                                    puerto_ser.setSerialPortParams(
                                            baudRate,
                                            SerialPort.DATABITS_8,
                                            SerialPort.STOPBITS_1,
                                            SerialPort.PARITY_NONE);
                                    puerto_ser.setDTR(true);
                 ////////////////////////////////////////////////////////////////
                                    out = puerto_ser.getOutputStream();//salida de java
                                    in = puerto_ser.getInputStream(); // entrada de java
                                    btnNewButton_1.setEnabled(true);
                                    btnNewButton.setEnabled(false);
                                    timer.resume(); //esta variable iniciará nuestro metodo ImplementoRunnable
                            } catch (  IOException e1) {
                            } catch (PortInUseException e1) {
                                e1.printStackTrace();
                            } catch (UnsupportedCommOperationException e1) {
                                e1.printStackTrace();
                            }
 
                         break;
                     }
                    }
            }
        });
        btnNewButton.setBounds(38, 63, 89, 23);
        contentPane.add(btnNewButton);
 
        btnNewButton_1 = new JButton("Desconectar");
        btnNewButton_1.setEnabled(false);
        btnNewButton_1.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent arg0) {
                    timer.interrupt();
                puerto_ser.close();
                btnNewButton_1.setEnabled(false);
                btnNewButton.setEnabled(true);
            }
        });
        btnNewButton_1.setBounds(205, 63, 128, 23);
        contentPane.add(btnNewButton_1);
 
        textField = new JTextField();
        textField.setBounds(38, 32, 86, 20);
        contentPane.add(textField);
        textField.setColumns(10);
 
        JLabel lblPuertoCom = new JLabel("Puerto COM");
        lblPuertoCom.setBounds(37, 11, 90, 14);
        contentPane.add(lblPuertoCom);
 
        lblNewLabel = new JLabel("VOLTAJE");
        lblNewLabel.setBounds(80, 124, 128, 24);
        lblNewLabel .setFont(new java.awt.Font("Arial", 0, 20));
        lblNewLabel .setForeground(Color.blue);
        contentPane.add(lblNewLabel);
    }public void paint(Graphics g) {
            super.paint(g);
        g.setColor(Color.blue);
        //g.fillRect(38, 250-temp, 20, temp);
        try {
            Thread.sleep(200);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }}
    private class ImplementoRunnable implements Runnable{
       int aux;
        public void run() {
            while(true){
                try {
             
                Thread.sleep(100);
                aux = in.read();
               
                //el puerto nos regresa el valor los sensores
             //if (aux!=2){
            	// if(aux!=-1){
              VOLTAJE = aux;
              lblNewLabel.setText(""+VOLTAJE); //lo imprimimos para mostrar el valor de la temperatura
            System.out.println(aux);
            repaint();//}
             //}
            } catch (Exception e1) {
            }}}}}
