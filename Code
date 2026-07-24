import javax.swing.*;
import javax.swing.table.DefaultTableModel;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.util.ArrayList;
import java.util.List;

public class StudentManagementSystem extends JFrame {


    private static class Student {
        String id, name, course;
        int age;
        double marks;

        Student(String id, String name, int age, String course, double marks) {
            this.id = id;
            this.name = name;
            this.age = age;
            this.course = course;
            this.marks = marks;
        }
    }

    private final List<Student> students = new ArrayList<>();

    private JTextField idField, nameField, ageField, courseField, marksField;
    private JTable table;
    private DefaultTableModel tableModel;

    public StudentManagementSystem() {
        setTitle("Student Management System");
        setSize(800, 500);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLocationRelativeTo(null);
        setLayout(new BorderLayout(10, 10));

        add(buildFormPanel(), BorderLayout.NORTH);
        add(buildTablePanel(), BorderLayout.CENTER);
        add(buildButtonPanel(), BorderLayout.SOUTH);
    }

    private JPanel buildFormPanel() {
        JPanel panel = new JPanel(new GridBagLayout());
        panel.setBorder(BorderFactory.createTitledBorder("Student Details"));
        GridBagConstraints gbc = new GridBagConstraints();
        gbc.insets = new Insets(6, 8, 6, 8);
        gbc.fill = GridBagConstraints.HORIZONTAL;

        idField = new JTextField(10);
        nameField = new JTextField(15);
        ageField = new JTextField(5);
        courseField = new JTextField(12);
        marksField = new JTextField(6);

        addFormRow(panel, gbc, 0, "Student ID:", idField, "Name:", nameField);
        addFormRow(panel, gbc, 1, "Age:", ageField, "Course:", courseField);

        gbc.gridx = 0;
        gbc.gridy = 2;
        panel.add(new JLabel("Marks:"), gbc);
        gbc.gridx = 1;
        panel.add(marksField, gbc);

        return panel;
    }

    private void addFormRow(JPanel panel, GridBagConstraints gbc, int row,
                             String label1, JComponent field1,
                             String label2, JComponent field2) {
        gbc.gridy = row;

        gbc.gridx = 0;
        panel.add(new JLabel(label1), gbc);
        gbc.gridx = 1;
        panel.add(field1, gbc);

        gbc.gridx = 2;
        panel.add(new JLabel(label2), gbc);
        gbc.gridx = 3;
        panel.add(field2, gbc);
    }

    private JPanel buildTablePanel() {
        JPanel panel = new JPanel(new BorderLayout());
        panel.setBorder(BorderFactory.createTitledBorder("Student Records"));

        String[] columns = {"ID", "Name", "Age", "Course", "Marks"};
        tableModel = new DefaultTableModel(columns, 0) {
            @Override
            public boolean isCellEditable(int row, int col) {
                return false; // records are edited via the form, not inline
            }
        };
        table = new JTable(tableModel);
        table.setRowHeight(24);
        table.getSelectionModel().addListSelectionListener(e -> loadSelectedRowIntoForm());

        panel.add(new JScrollPane(table), BorderLayout.CENTER);
        return panel;
    }

    private JPanel buildButtonPanel() {
        JPanel panel = new JPanel(new FlowLayout(FlowLayout.CENTER, 12, 10));

        JButton addBtn = new JButton("Add Student");
        JButton updateBtn = new JButton("Update Student");
        JButton deleteBtn = new JButton("Delete Student");
        JButton clearBtn = new JButton("Clear Form");

        addBtn.addActionListener(this::onAdd);
        updateBtn.addActionListener(this::onUpdate);
        deleteBtn.addActionListener(this::onDelete);
        clearBtn.addActionListener(e -> clearForm());

        panel.add(addBtn);
        panel.add(updateBtn);
        panel.add(deleteBtn);
        panel.add(clearBtn);
        return panel;
    }

    private void onAdd(ActionEvent e) {
        Student s = readFormAsStudent();
        if (s == null) return;

        if (findStudentIndex(s.id) != -1) {
            showError("A student with this ID already exists. Use Update instead.");
            return;
        }

        students.add(s);
        refreshTable();
        clearForm();
    }

    private void onUpdate(ActionEvent e) {
        Student s = readFormAsStudent();
        if (s == null) return;

        int index = findStudentIndex(s.id);
        if (index == -1) {
            showError("No student found with this ID. Use Add instead.");
            return;
        }

        students.set(index, s);
        refreshTable();
        clearForm();
    }

    private void onDelete(ActionEvent e) {
        int row = table.getSelectedRow();
        if (row == -1) {
            showError("Select a record from the table to delete.");
            return;
        }
        String id = (String) tableModel.getValueAt(row, 0);
        students.removeIf(s -> s.id.equals(id));
        refreshTable();
        clearForm();
    }

    private Student readFormAsStudent() {
        String id = idField.getText().trim();
        String name = nameField.getText().trim();
        String course = courseField.getText().trim();
        String ageText = ageField.getText().trim();
        String marksText = marksField.getText().trim();

        if (id.isEmpty() || name.isEmpty() || course.isEmpty()
                || ageText.isEmpty() || marksText.isEmpty()) {
            showError("Please fill in all fields.");
            return null;
        }

        int age;
        double marks;
        try {
            age = Integer.parseInt(ageText);
            marks = Double.parseDouble(marksText);
        } catch (NumberFormatException ex) {
            showError("Age must be a whole number and Marks must be numeric.");
            return null;
        }

        return new Student(id, name, age, course, marks);
    }

    private int findStudentIndex(String id) {
        for (int i = 0; i < students.size(); i++) {
            if (students.get(i).id.equals(id)) return i;
        }
        return -1;
    }

    private void refreshTable() {
        tableModel.setRowCount(0);
        for (Student s : students) {
            tableModel.addRow(new Object[]{s.id, s.name, s.age, s.course, s.marks});
        }
    }

    private void loadSelectedRowIntoForm() {
        int row = table.getSelectedRow();
        if (row == -1) return;

        idField.setText(tableModel.getValueAt(row, 0).toString());
        nameField.setText(tableModel.getValueAt(row, 1).toString());
        ageField.setText(tableModel.getValueAt(row, 2).toString());
        courseField.setText(tableModel.getValueAt(row, 3).toString());
        marksField.setText(tableModel.getValueAt(row, 4).toString());
    }

    private void clearForm() {
        idField.setText("");
        nameField.setText("");
        ageField.setText("");
        courseField.setText("");
        marksField.setText("");
        table.clearSelection();
        idField.requestFocus();
    }

    private void showError(String message) {
        JOptionPane.showMessageDialog(this, message, "Input Error", JOptionPane.ERROR_MESSAGE);
    }
    public static void main(String[] args) {
        try {
            UIManager.setLookAndFeel(UIManager.getSystemLookAndFeelClassName());
        } catch (Exception ignored) {
            // fall back to default look and feel
        }
        SwingUtilities.invokeLater(() -> new StudentManagementSystem().setVisible(true));
    }
}
