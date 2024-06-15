# IMC

package imc;
/**
 *
 * @author Valber José Costa
 * Calculador IMC - atividade ciclo 3 POO UNIS
 */
import javax.swing.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class CalculadoraIMC extends JFrame {
    private JTextField textFieldPeso;
    private JTextField textFieldAltura;
    private final JButton calcularButton;
    private JTextArea textAreaResultado;

    public CalculadoraIMC() {
        setTitle("Calculadora de IMC");
        setSize(300, 200);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(new BoxLayout(getContentPane(), BoxLayout.Y_AXIS));

        textFieldPeso = new JTextField();
        textFieldAltura = new JTextField();
        calcularButton = new JButton("Calcular");
        textAreaResultado = new JTextArea();

        add(new JLabel("Peso em Kg:"));
        add(textFieldPeso);
        add(new JLabel("Altura em Cm:"));
        add(textFieldAltura);
        add(calcularButton);
        add(new JScrollPane(textAreaResultado));

        calcularButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                try {
                    double peso = Double.parseDouble(textFieldPeso.getText());
                    double altura = Double.parseDouble(textFieldAltura.getText()) / 100; // Convertendo para metros
                    double imc = peso / (altura * altura);
                    String classificacao = getClassificacaoIMC(imc);
                    textAreaResultado.setText(String.format("Seu IMC é: %.2f\nClassificação: %s", imc, classificacao));
                } catch (NumberFormatException ex) {
                    JOptionPane.showMessageDialog(CalculadoraIMC.this,
                            "Por favor, insira números válidos para peso e altura.",
                            "Erro de Formato",
                            JOptionPane.ERROR_MESSAGE);
                }
            }
        });
    }

    private String getClassificacaoIMC(double imc) {
        if (imc < 18.5) {
            return "Abaixo do peso";
        } else if (imc < 25) {
            return "Peso normal";
        } else if (imc < 30) {
            return "Sobrepeso";
        } else {
            return "Obesidade";
        }
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> new CalculadoraIMC().setVisible(true));
    }
}
