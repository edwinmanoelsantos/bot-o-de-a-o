# bot-o-de-acao

import javax.swing.*; 
import java.awt.*;
import java.awt.event.*;

public class AplicacaoSwing implements ActionListener {
 private static String labelPrefix = "Numero de cliques de botao: ";
 private int numClicks = 0;
 final JLabel label = new JLabel(labelPrefix + "0 ");


 final static String LOOKANDFEEL = "System";

 public Component createComponents() {
 JButton button = new JButton("Eu sou um botao Swing!");
 button.setMnemonic(KeyEvent.VK_I);
 button.addActionListener(this);
 label.setLabelFor(button);


 JPanel pane = new JPanel(new GridLayout(0, 1));
 pane.add(button);
 pane.add(label);
 pane.setBorder(BorderFactory.createEmptyBorder(
 30, 
 30, 
 10, 
 30) 
 );

 return pane;
 }

 public void actionPerformed(ActionEvent e) {
 numClicks++;
 label.setText(labelPrefix + numClicks);
 }

 private static void initLookAndFeel() {
 String lookAndFeel = null;

 if (LOOKANDFEEL != null) {
 if (LOOKANDFEEL.equals("Metal")) {
 lookAndFeel = UIManager.getCrossPlatformLookAndFeelClassName();
 } else if (LOOKANDFEEL.equals("System")) {
 lookAndFeel = UIManager.getSystemLookAndFeelClassName();
 } else if (LOOKANDFEEL.equals("Motif")) {
 lookAndFeel = "com.sun.java.swing.plaf.motif.MotifLookAndFeel";
 } else if (LOOKANDFEEL.equals("GTK+")) { //novo a partir da versao 1.4.2
 lookAndFeel = "com.sun.java.swing.plaf.gtk.GTKLookAndFeel";
 } else {
 System.err.println("Valor inesperado de especifico LOOKANDFEEL: "
 + LOOKANDFEEL);
 lookAndFeel = UIManager.getCrossPlatformLookAndFeelClassName();
 }

 try {
 UIManager.setLookAndFeel(lookAndFeel);
 } catch (ClassNotFoundException e) {
 System.err.println("Nao pode encontrar classe especifica para o look and feel:"
 + lookAndFeel);
 System.err.println("Voce incluiu a biblioteca L&F library no class path?");
 System.err.println("Usa o padrao look and feel.");
 } catch (UnsupportedLookAndFeelException e) {
 System.err.println("Nao pode ser especificado um look and feel ("
 + lookAndFeel
 + ") nesta plataforma.");
 System.err.println("Uso do padrao look and feel.");
 } catch (Exception e) {
 System.err.println("Nao pode obter especifico look and feel ("
 + lookAndFeel
 + "), por alguma razao .");
 System.err.println("Uso do padrao look and feel.");
 e.printStackTrace();
 }
 }
 }


 private static void criaExibeGUI() {

 initLookAndFeel();


 JFrame.setDefaultLookAndFeelDecorated(true);

 
 JFrame frame = new JFrame("AplicacaoSwing");
 frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

 AplicacaoSwing app = new AplicacaoSwing();
 Component contents = app.createComponents();
 frame.getContentPane().add(contents, BorderLayout.CENTER);


 frame.pack();
 frame.setVisible(true);
 }

 public static void main(String[] args) {
 
 javax.swing.SwingUtilities.invokeLater(new Runnable() {
 public void run() {
 criaExibeGUI();
 }
 });
 }
}
