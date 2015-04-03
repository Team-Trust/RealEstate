# RealEstate
public Class Real Estate
import java.awt.*;
import java.awt.event.*;
import java.io.*;
import java.text.SimpleDateFormat;
import java.util.ArrayList;
import java.util.Date;
import javaapplication6.ListHouse;
import javax.swing.*;
import javax.swing.border.*;

public class main extends JFrame {

    static ArrayList<ListHouse> al = null;
    // the list of house information
    
    //* @author BUDDHINI
    private static JTextField lotText;            
    private static JTextField firstText;          
    private static JTextField lastText;     
    private static JTextField priceText;          
    private static JTextField feetText;       
    private static JTextField bedText;              
    private static JLabel statusLabel;      

    
    // Clears house information from screen
    private static void clearHouse() {
    }
    // Define a button listener
    static int j = 1;

    private static class ActionHandler implements ActionListener {

        public void actionPerformed(ActionEvent event) // Listener for the button events
        {
            if (event.getActionCommand().equals("Reset")) { // Handles Reset event
                clear();
            } else if (event.getActionCommand().equals("Next")) { // Handles Next event

                ListHouse ll = main.getOnehouse1(j);
                if (ll == null) {
                    JOptionPane.showMessageDialog(null, "Result Not Found");
                } else {
                    lotText.setText(ll.getId() + "");
                    firstText.setText(ll.getFname());
                    lastText.setText(ll.getLname());
                    priceText.setText(ll.getPrice() + "");
                    feetText.setText(ll.getSquareFeet() + "");
                    bedText.setText(ll.getBedRooms() + "");
                }
                j++;
            } else if (event.getActionCommand().equals("Add")) { // Handles Add event
                ListHouse house = new ListHouse();
                house.setId(Integer.parseInt(lotText.getText()));
                house.setFname(firstText.getText());
                house.setLname(lastText.getText());
                house.setPrice(Integer.parseInt(priceText.getText()));
                house.setSquareFeet(Integer.parseInt(feetText.getText()));
                house.setBedRooms(Integer.parseInt(bedText.getText()));

                if (al == null) {
                    al = new ArrayList<>();
                    al.add(house);
                } else {
                    al.add(house);
                }

//                new SortedList().setHouse(house);

            } else if (event.getActionCommand().equals("Delete")) { //Handels the Delete Event
                int id = Integer.parseInt(lotText.getText());
                al.remove(id);
            } else if (event.getActionCommand().equals("Clear")) { // Handles Clear event
                clear();
            } else if (event.getActionCommand().equals("Find")) { // Handles Find event
                int id = Integer.parseInt(lotText.getText());
                ListHouse ll = main.getOnehouse1(id);
                if (ll == null) {
                    JOptionPane.showMessageDialog(null, "No Result Found");
                } else {
                    lotText.setText(ll.getId() + "");
                    firstText.setText(ll.getFname());
                    lastText.setText(ll.getLname());
                    priceText.setText(ll.getPrice() + "");
                    feetText.setText(ll.getSquareFeet() + "");
                    bedText.setText(ll.getBedRooms() + "");

                }
            }
        }

        private void clear() {
            lotText.setText("");
            firstText.setText("");
            lastText.setText("");
            priceText.setText("");
            feetText.setText("");
            bedText.setText("");

            j = 1;
        }
    }

    public static void main(String args[]) throws IOException {

        char command;
        int length;

        JLabel blankLabel;         

        JLabel lotLabel;           
        JLabel firstLabel;
        JLabel lastLabel;
        JLabel priceLabel;
        JLabel feetLabel;
        JLabel bedLabel;

        JButton reset;             // Reset button
        JButton next;	       // Next button
        JButton add;               // Add button
        JButton delete;            // Delete button
        JButton clear;             // Clear button
        JButton find;              // Find button
        ActionHandler action;      // Declare listener

        // Declare/instantiate/initialize display frame
        JFrame displayFrame = new JFrame();
        displayFrame.setTitle("Real Estate Program");
        displayFrame.setSize(350, 400);
        displayFrame.addWindowListener(new WindowAdapter() // handle window closing
        {
            public void windowClosing(WindowEvent event) {
                ListHouse house;
                try {
                    String date = new SimpleDateFormat("HHmmssddMMyyyy").format(new Date());
                    String path = "D:/Print/" + date + ".txt";
                    File file = new File(path);
                    FileOutputStream fos = new FileOutputStream(file);
                    ObjectOutputStream oos = new ObjectOutputStream(fos);
                    oos.writeInt(al.size());
                } catch (Exception e) {
                    e.printStackTrace();
                }
                System.exit(0);                           // Quit the program
            }
        });

        // Instantiate content pane and information panel
        Container contentPane = displayFrame.getContentPane();
        JPanel infoPanel = new JPanel();

        // Instantiate/initialize labels, and text fields
        statusLabel = new JLabel("", JLabel.CENTER);
        statusLabel.setBorder(new LineBorder(Color.red));
        blankLabel = new JLabel("");
        lotLabel = new JLabel("Lot Number:  ", JLabel.RIGHT);
        lotText = new JTextField("", 15);
        firstLabel = new JLabel("First Name:  ", JLabel.RIGHT);
        firstText = new JTextField("", 15);
        lastLabel = new JLabel("Last Name:  ", JLabel.RIGHT);
        lastText = new JTextField("", 15);
        priceLabel = new JLabel("Price:  ", JLabel.RIGHT);
        priceText = new JTextField("", 15);
        feetLabel = new JLabel("Square Feet:  ", JLabel.RIGHT);
        feetText = new JTextField("", 15);
        bedLabel = new JLabel("Number of Bedrooms:  ", JLabel.RIGHT);
        bedText = new JTextField("", 15);

        // Instantiate/register buttons
        reset = new JButton("Reset");
        next = new JButton("Next");
        add = new JButton("Add");
        delete = new JButton("Delete");
        clear = new JButton("Clear");
        find = new JButton("Find");

        // Instantiate/register button listeners
        action = new ActionHandler();
        reset.addActionListener(action);
        next.addActionListener(action);
        add.addActionListener(action);
        delete.addActionListener(action);
        clear.addActionListener(action);
        find.addActionListener(action);




        // Add components to frame
        infoPanel.setLayout(new GridLayout(10, 2));
        infoPanel.add(statusLabel);
        infoPanel.add(blankLabel);
        infoPanel.add(lotLabel);
        infoPanel.add(lotText);
        infoPanel.add(firstLabel);
        infoPanel.add(firstText);
        infoPanel.add(lastLabel);
        infoPanel.add(lastText);
        infoPanel.add(priceLabel);
        infoPanel.add(priceText);
        infoPanel.add(feetLabel);
        infoPanel.add(feetText);
        infoPanel.add(bedLabel);
        infoPanel.add(bedText);
        infoPanel.add(reset);
        infoPanel.add(next);
        infoPanel.add(add);
        infoPanel.add(delete);
        infoPanel.add(clear);
        infoPanel.add(find);

      
        contentPane.add(infoPanel);
        displayFrame.show();

    }

    public static ListHouse getOnehouse1(int id) {
        ListHouse house = null;
        ArrayList<ListHouse> al = main.al;

        for (ListHouse listHouse : al) {
            if (listHouse.getId() == id) {
                house = al.get(id - 1);
            }
        }
        return house;
    }
}

