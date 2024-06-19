import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class Calculator implements ActionListener {

    JFrame frame;
    JTextField textField;
    JButton[] numberButtons = new JButton[10];
    JButton[] operatorButtons = new JButton[5];
    JButton clearButton, equalsButton;
    JPanel panel;
    double number1, number2, result;
    char operation;

    Calculator() {
        frame = new JFrame("Calculator");
        frame.setSize(200, 250);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setLayout(new FlowLayout());

        textField = new JTextField(20);
        frame.add(textField);

        for (int i = 0; i < 10; i++) {
            numberButtons[i] = new JButton(String.valueOf(i));
            numberButtons[i].addActionListener(this);
            frame.add(numberButtons[i]);
        }

        String[] operators = {"+", "-", "*", "/"};
        for (int i = 0; i < 4; i++) {
            operatorButtons[i] = new JButton(operators[i]);
            operatorButtons[i].addActionListener(this);
            frame.add(operatorButtons[i]);
        }

        clearButton = new JButton("C");
        clearButton.addActionListener(this);
        frame.add(clearButton);

        equalsButton = new JButton("=");
        equalsButton.addActionListener(this);
        frame.add(equalsButton);

        frame.setVisible(true);
    }

    public void actionPerformed(ActionEvent e) {
        for (int i = 0; i < 10; i++) {
            if (e.getSource() == numberButtons[i]) {
                textField.setText(textField.getText() + i);
            }
        }

        for (int i = 0; i < 4; i++) {
            if (e.getSource() == operatorButtons[i]) {
                number1 = Double.parseDouble(textField.getText());
                operation = operators[i].charAt(0);
                textField.setText("");
            }
        }

        if (e.getSource() == clearButton) {
            textField.setText("");
        }

        if (e.getSource() == equalsButton) {
            number2 = Double.parseDouble(textField.getText());
            switch (operation) {
                case '+':
                    result = number1 + number2;
                    break;
                case '-':
                    result = number1 - number2;
                    break;
                case '*':
                    result = number1 * number2;
                    break;
                case '/':
                    result = number1 / number2;
                    break;
            }
            textField.setText(String.valueOf(result));
        }
    }

    public static void main(String[] args) {
        new Calculator();
    }
}
