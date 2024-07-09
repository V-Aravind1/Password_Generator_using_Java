# Password_Generator_using_Java
Designing and developing the unique passwords with the given input cases using Java programming language.

import java.awt.Color;
import java.awt.Cursor;
import java.awt.FlowLayout;
import java.awt.Font;
import java.awt.GridLayout;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.util.Random;
import javax.swing.BorderFactory;
import javax.swing.JButton;
import javax.swing.JCheckBox;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JOptionPane;
import javax.swing.JPanel;
import javax.swing.JSpinner;
import javax.swing.JTextField;
import javax.swing.SpinnerNumberModel;
import javax.swing.SwingUtilities;
import javax.swing.UIManager;

public class Password_Generator_App extends JFrame {

    private JCheckBox LowerCaseCheckBox;
    private JCheckBox UpperCaseCheckBox;
    private JCheckBox NumbersCheckBox;
    private JCheckBox SpecialCharsCheckBox;
    private JSpinner LengthSpinner;
    private JTextField PasswordTextField;
    private JButton GenerateButton;
    
    public Password_Generator_App(){
        // Set up the JFrame properties
        setTitle("Password Generator");
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setSize(400,400);
        setLocationRelativeTo(null);
        initialize(); // initialize the user interface
    }
    
    private void initialize(){
        // Create checkboxes for character type selection
        LowerCaseCheckBox = new JCheckBox("Include LowerCase");
        UpperCaseCheckBox = new JCheckBox("Include UpperCase");
        NumbersCheckBox = new JCheckBox("Include Numbers");
        SpecialCharsCheckBox = new JCheckBox("Include Special Characters");
        
        LowerCaseCheckBox.setFocusPainted(false);
        LowerCaseCheckBox.setBorderPainted(false);
        LowerCaseCheckBox.setCursor(new Cursor(Cursor.HAND_CURSOR));
        
        UpperCaseCheckBox.setFocusPainted(false);
        UpperCaseCheckBox.setBorderPainted(false);
        UpperCaseCheckBox.setCursor(new Cursor(Cursor.HAND_CURSOR));
        
        NumbersCheckBox.setFocusPainted(false);
        NumbersCheckBox.setBorderPainted(false);
        NumbersCheckBox.setCursor(new Cursor(Cursor.HAND_CURSOR));
        
        SpecialCharsCheckBox.setFocusPainted(false);
        SpecialCharsCheckBox.setBorderPainted(false);
        SpecialCharsCheckBox.setCursor(new Cursor(Cursor.HAND_CURSOR));
        
        // Create a spinner for password length selection
        LengthSpinner = new JSpinner(new SpinnerNumberModel(8,4,20,1));
        
        // Create a text field to display the generated password
        PasswordTextField = new JTextField(20);
        PasswordTextField.setFont(new Font("Arial", Font.PLAIN, 16));
        PasswordTextField.setEditable(false);
        
        // Create a button to generate passwords
        GenerateButton = new JButton("Generate Password");
        GenerateButton.setBackground(new Color(63,81,181));
        GenerateButton.setForeground(Color.white);
        GenerateButton.setFocusPainted(false);
        GenerateButton.setBorderPainted(false);
        GenerateButton.setCursor(new Cursor(Cursor.HAND_CURSOR));
        
        GenerateButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
            
                generatePassword();
                
            }
        });
        
        // Create panels to hold UI components
        JPanel MainPanel = new JPanel(new GridLayout(8,1,10,10));
        MainPanel.setBorder(BorderFactory.createEmptyBorder(20,20,20,20));
        MainPanel.setBackground(Color.white);
        
        MainPanel.add(LowerCaseCheckBox);
        MainPanel.add(UpperCaseCheckBox);
        MainPanel.add(NumbersCheckBox);
        MainPanel.add(SpecialCharsCheckBox);
        
        JPanel LengthPanel = new JPanel(new FlowLayout(FlowLayout.LEFT));
        LengthPanel.setBackground(Color.white);
        LengthPanel.add(new JLabel("Password Length"));
        LengthPanel.add(LengthSpinner);
        MainPanel.add(LengthPanel);
        
        JPanel ButtonPanel = new JPanel(new FlowLayout(FlowLayout.CENTER));
        ButtonPanel.setBackground(Color.white);
        ButtonPanel.add(GenerateButton);
        MainPanel.add(ButtonPanel);
        MainPanel.add(PasswordTextField);
        
        getContentPane().setBackground(Color.white);
        add(MainPanel);
        
    }
    
    
    private String generatePassword()
    {
        // Get the desired password length from the spinner
        int passwordLength = (int) LengthSpinner.getValue();
        
        // Define character sets for password generation
        String lowerCase = "abcdefghijklmnopqrstuvwxyz";
        String upperCase = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
        String numbers = "0123456789";
        String specialChars = "!@#$%^&*()_+-=[]{}|;:,.<>?";
        
        
        // Initialize the characters string based on user selections
        String Characters = "";
        if(LowerCaseCheckBox.isSelected()) Characters += lowerCase;
        if(UpperCaseCheckBox.isSelected()) Characters += upperCase;
        if(NumbersCheckBox.isSelected()) Characters += numbers;
        if(SpecialCharsCheckBox.isSelected()) Characters += specialChars;
        
        // If no character type is selected, show an error message
        if (Characters.isEmpty())
        {
            JOptionPane.showMessageDialog(this, "Please Select at Least one Character type");
            return "";
        }
        
        // Generate the password by selecting random characters from the characters string
        Random random = new Random();
        StringBuilder password = new StringBuilder();
        for(int i = 0; i < passwordLength; i++)
        {
           int randomIndex = random.nextInt(Characters.length());
           char randomChar = Characters.charAt(randomIndex);
           password.append(randomChar);
        }
        
        // Display the generated password in the text field
        PasswordTextField.setText(password.toString());
        return password.toString();
        
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> {
            try
            {
                UIManager.setLookAndFeel("javax.swing.plaf.metal.MetalLookAndFeel");
            }
            catch(Exception ex)
            {
                ex.printStackTrace();
            } 
            Password_Generator_App app = new Password_Generator_App();
            app.setVisible(true);
        
        });        
    }
}![Without-Upper Case](https://github.com/V-Aravind1/Password_Generator_using_Java/assets/175092697/6bf34eba-a4c9-4f87-83a5-9c28fdfdc5cd)
![Without-Special Char](https://github.com/V-Aravind1/Password_Generator_using_Java/assets/175092697/83982c63-05c4-4c77-989b-4dc21e0840ee)
![Uploading Without-Lower Case.png…]()
![Without- Number](https://github.com/V-Aravind1/Password_Generator_using_Java/assets/175092697/61c9f9f4-036e-4120-8fa9-6e43198ac646)
![With-All Cases-2](https://github.com/V-Aravind1/Password_Generator_using_Java/assets/175092697/ed48da79-2226-40c6-80b6-6ed1942e2b27)
![With-All Cases-1](https://github.com/V-Aravind1/Password_Generator_using_Java/assets/175092697/c3d87002-bad0-4f2a-8603-f3c091a95a9a)
