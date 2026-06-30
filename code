# GUI---Calculator
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;
import javax.script.ScriptEngineManager;
import javax.script.ScriptEngine;
import javax.script.ScriptException;

public class AdvancedStringCalculator extends JFrame implements ActionListener {

    private JTextField display;
    private StringBuilder input = new StringBuilder();
    private ScriptEngine engine;

    public AdvancedStringCalculator() {
     
        setTitle("Advanced Calculator");
        setSize(400, 550);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(new BorderLayout());

        engine = new ScriptEngineManager().getEngineByName("JavaScript");

        display = new JTextField();
        display.setFont(new Font("Consolas", Font.BOLD, 28));
        display.setHorizontalAlignment(SwingConstants.RIGHT);
        display.setEditable(false);
        display.setBackground(Color.WHITE);
        add(display, BorderLayout.NORTH);

        String[] buttonLabels = {
            "C", "⌫", "%", "/",
            "7", "8", "9", "*",
            "4", "5", "6", "-",
            "1", "2", "3", "+",
            "+/-", "0", ".", "=",
            "x²", "√", "1/x"
        };

        JPanel panel = new JPanel();
        panel.setLayout(new GridLayout(6, 4, 10, 10));
        panel.setBackground(Color.DARK_GRAY);

        for (String text : buttonLabels) {
            JButton button = new JButton(text);
            button.setFont(new Font("Arial", Font.BOLD, 20));
            button.setBackground(Color.LIGHT_GRAY);
            button.addActionListener(this);
            panel.add(button);
        }

        add(panel, BorderLayout.CENTER);
        setVisible(true);
    }

    @Override
    public void actionPerformed(ActionEvent e) {
        String command = e.getActionCommand();

        try {
            switch (command) {
                case "C":
                    input.setLength(0);
                    display.setText("");
                    break;

                case "⌫":
                    if (input.length() > 0) {
                        input.deleteCharAt(input.length() - 1);
                        display.setText(input.toString());
                    }
                    break;

                case "=":
                    evaluateExpression();
                    break;

                case "+/-":
                    toggleSign();
                    break;

                case "x²":
                    squareNumber();
                    break;

                case "√":
                    squareRoot();
                    break;

                case "1/x":
                    reciprocal();
                    break;

                default:
                    input.append(command);
                    display.setText(input.toString());
                    break;
            }
        } catch (Exception ex) {
            display.setText("Error");
            input.setLength(0);
        }
    }

    private void evaluateExpression() {
        try {
            String expression = input.toString();
            Object result = engine.eval(expression);
            display.setText(result.toString());
            input.setLength(0);
            input.append(result);
        } catch (ScriptException e) {
            display.setText("Error");
            input.setLength(0);
        }
    }

    private void toggleSign() {
        if (input.length() == 0) return;
        String value = input.toString();
        try {
            double num = Double.parseDouble(value);
            num = -num;
            input.setLength(0);
            input.append(num);
            display.setText(input.toString());
        } catch (Exception e) {
            display.setText("Error");
        }
    }

    private void squareNumber() {
        try {
            double num = Double.parseDouble(display.getText());
            double result = num * num;
            display.setText(String.valueOf(result));
            input.setLength(0);
            input.append(result);
        } catch (Exception e) {
            display.setText("Error");
        }
    }

    private void squareRoot() {
        try {
            double num = Double.parseDouble(display.getText());
            if (num < 0) throw new ArithmeticException();
            double result = Math.sqrt(num);
            display.setText(String.valueOf(result));
            input.setLength(0);
            input.append(result);
        } catch (Exception e) {
            display.setText("Error");
        }
    }

    private void reciprocal() {
        try {
            double num = Double.parseDouble(display.getText());
            if (num == 0) throw new ArithmeticException();
            double result = 1 / num;
            display.setText(String.valueOf(result));
            input.setLength(0);
            input.append(result);
        } catch (Exception e) {
            display.setText("Error");
        }
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> new AdvancedStringCalculator());
    }
}
