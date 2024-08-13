# Online-Examination-System
# Online Examination System using GUI
package MyFirstProject;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import javax.swing.ButtonGroup;
import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JOptionPane;
import javax.swing.JRadioButton;

class OnlineTest extends JFrame implements ActionListener {
	
	private static final long serialVersionUID = 1L;

	JLabel label;
	JRadioButton radioButton[] = new JRadioButton[5];
	JButton btnNext, btnBookmark;
	ButtonGroup bg;
	int count = 0, current = 0, x = 1, y = 1, now = 0;
	int m[] = new int[10];

	// create jFrame with radioButton and JButton
	OnlineTest(String s) {
		super(s);
		label = new JLabel();
		add(label);
		bg = new ButtonGroup();
		for (int i = 0; i < 5; i++) {
			radioButton[i] = new JRadioButton();
			add(radioButton[i]);
			bg.add(radioButton[i]);
		}
		btnNext = new JButton("Next");
		btnBookmark = new JButton("Bookmark");
		btnNext.addActionListener(this);
		btnBookmark.addActionListener(this);
		add(btnNext);
		add(btnBookmark);
		set();
		label.setBounds(30, 40, 450, 20);
		//radioButton[0].setBounds(50, 80, 200, 20);
		radioButton[0].setBounds(50, 80, 450, 20);
		radioButton[1].setBounds(50, 110, 200, 20);
		radioButton[2].setBounds(50, 140, 200, 20);
		radioButton[3].setBounds(50, 170, 200, 20);
		btnNext.setBounds(100, 240, 100, 30);
		btnBookmark.setBounds(270, 240, 100, 30);
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		setLayout(null);
		setLocation(250, 100);
		setVisible(true);
		setSize(600, 350);
	}

	// handle all actions based on event
	public void actionPerformed(ActionEvent e) {
		if (e.getSource() == btnNext) {
			if (check())
				count = count + 1;
			current++;
			set();
			if (current == 4) {
				btnNext.setEnabled(false);
				btnBookmark.setText("Result");
			}
		}
		if (e.getActionCommand().equals("Bookmark")) {
			JButton bk = new JButton("Bookmark" + x);
			bk.setBounds(480, 20 + 30 * x, 100, 30);
			add(bk);
			bk.addActionListener(this);
			m[x] = current;
			x++;
			current++;
			set();
			if (current == 4)
				btnBookmark.setText("Result");
			setVisible(false);
			setVisible(true);
		}
		for (int i = 0, y = 1; i < x; i++, y++) {
			if (e.getActionCommand().equals("Bookmark" + y)) {
				if (check())
					count = count + 1;
				now = current;
				current = m[y];
				set();
				((JButton) e.getSource()).setEnabled(false);
				current = now;
			}
		}

		if (e.getActionCommand().equals("Result")) {
			if (check())
				count = count + 1;
			current++;
			JOptionPane.showMessageDialog(this, "correct answers= " + count);
			System.exit(0);
		}
	}

	// SET Questions with options
	void set() {
		radioButton[4].setSelected(true);
		if (current == 0) {
			label.setText("Que1: Who invented Java Programming?  ");
			radioButton[0].setText(" Guido van Rossum");
			radioButton[1].setText(" James Gosling");
			radioButton[2].setText(" Dennis Ritchie");
			radioButton[3].setText(" Bjarne Stroustrup");
		}
		if (current == 1) {
			label.setText("Que2: Which component is used to compile & execute the java programs?");
			radioButton[0].setText(" JRE");
			radioButton[1].setText(" JIT");
			radioButton[2].setText(" JDK");
			radioButton[3].setText(" JVM");
		}
		if (current == 2) {
			label.setText("Que3: What is the extension of java code files?");
			radioButton[0].setText(" .js");
			radioButton[1].setText(" .txt");
			radioButton[2].setText(" .class");
			radioButton[3].setText(" .java");
		}
		if (current == 3) {
			label.setText("Que4: Which of the following is not an OOPS concept in Java?");
			radioButton[0].setText(" Polymorphism");
			radioButton[1].setText(" Inheritance");
			radioButton[2].setText(" Compilation");
			radioButton[3].setText(" Encapsulation");
		}
		if (current == 4) {
			label.setText("Que5: When is the object created with new keyword?");
			radioButton[0].setText(" At run time");
			radioButton[1].setText(" At compile time");
			radioButton[2].setText(" Depends on the code");
			radioButton[3].setText(" None");
		}
		
		label.setBounds(30, 40, 450, 20);
		for (int i = 0, j = 0; i <= 90; i += 30, j++)
			radioButton[j].setBounds(50, 80 + i, 200, 20);
	}

	// declare right answers.
	boolean check() {
		if (current == 0)
			return (radioButton[1].isSelected());
		if (current == 1)
			return (radioButton[2].isSelected());
		if (current == 2)
			return (radioButton[3].isSelected());
		if (current == 3)
			return (radioButton[2].isSelected());
		if (current == 4)
			return (radioButton[0].isSelected());
		
		return false;
	}

	public static void main(String s[]) {
		new OnlineTest("Online Test App");
	}

}
    

