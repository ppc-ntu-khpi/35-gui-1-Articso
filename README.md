# UI Lab 3
**Запуск [SWINGdemo.java](https://github.com/ppc-ntu-khpi/GUI-Lab1-Starter/blob/master/Lab%203%20-%20SWING/SWINGDemo.java) з цього репозиторію:**  
<img src="https://github.com/ppc-ntu-khpi/35-gui-1-Articso/blob/master/images/screen1.png"/>

# Завдання "На п'ять"
>Додайте ще одну кнопку - Report, яка має виводити у нижній частині вікна звіт за клієнтами такого ж виду, як у роботі номер 8 (див. CustomerReport).

**Код файлу** ```SWINGdemo.java```**:**  

```java
package com.mybank.gui;

import com.mybank.domain.Bank;
import com.mybank.domain.CheckingAccount;
import com.mybank.domain.Customer;
import com.mybank.domain.SavingsAccount;
import java.awt.BorderLayout;
import java.awt.Dimension;
import java.awt.GridLayout;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import javax.swing.JButton;
import javax.swing.JComboBox;
import javax.swing.JEditorPane;
import javax.swing.JFrame;
import javax.swing.JPanel;

/**
 *
 * @author Alexander 'Taurus' Babich
 */
public class SWINGDemo {
    
    private final JEditorPane log;
    private final JEditorPane reportCust;
    private final JButton show;
    private final JButton report;
    //private final JComboBox<String> clients;
    private final JComboBox clients;
    
    public SWINGDemo() {
        log = new JEditorPane("text/html", "");
        reportCust = new JEditorPane("text/html", "");
        log.setPreferredSize(new Dimension(250, 550));
        show = new JButton("Show");
        report = new JButton("Report");
        clients = new JComboBox();
        for (int i=0; i<Bank.getNumberOfCustomers();i++)
        {
            clients.addItem(Bank.getCustomer(i).getLastName()+", "+Bank.getCustomer(i).getFirstName());
        }
        
    }
    
    private void launchFrame() {
        JFrame frame = new JFrame("MyBank clients");
        frame.setLayout(new BorderLayout());
        JPanel cpane = new JPanel();
        cpane.setLayout(new GridLayout(1, 2));
        
        cpane.add(clients);
        cpane.add(show);
        cpane.add(report);
        frame.add(cpane, BorderLayout.NORTH);
        frame.add(log, BorderLayout.CENTER);
        frame.add(reportCust, BorderLayout.AFTER_LAST_LINE);
        
        show.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                Customer current = Bank.getCustomer(clients.getSelectedIndex());
                String accType = current.getAccount(0)instanceof CheckingAccount?"Checking":"Savings";                
                String custInfo="<br>&nbsp;<b><span style=\"font-size:2em;\">"+current.getLastName()+", "+
                        current.getFirstName()+"</span><br><hr>"+
                        "&nbsp;<b>Acc Type: </b>"+accType+
                        "<br>&nbsp;<b>Balance: <span style=\"color:red;\">$"+current.getAccount(0).getBalance()+"</span></b>";
                log.setText(custInfo);                
            }
        });
        
        report.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                String report = "&nbsp;<span style=\"font-size:1.5em;\"><b>CUSTOMERS REPORT</b></span>";
                for(int i = 0; i < Bank.getNumberOfCustomers(); i++) {
                    Customer customer = Bank.getCustomer(i);
                    report += "<hr><b>&nbsp;<span style=\"font-size:1em;\">"+customer.getLastName()+", "+customer.getFirstName()+"</span></b><br>";
                    for(int j = 0; j < customer.getNumberOfAccounts(); j++) {
                        String accType = customer.getAccount(j)instanceof CheckingAccount?"Checking":"Savings";
                        report += "&nbsp;<b>Acc Type: </b>"+accType+
                            "<br>&nbsp;<b>Balance: <span style=\"color:red;\">$"+customer.getAccount(j).getBalance()+"<br></span></b><br>";
                    }
                }
            reportCust.setText(report);                
            }
        });
   
        frame.pack();
        frame.setLocationRelativeTo(null);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);  
        frame.setResizable(false);
        frame.setVisible(true);        
    }
    
    public static void main(String[] args) {
        Bank.addCustomer("John", "Doe");
        Bank.addCustomer("Fox", "Mulder");
        Bank.addCustomer("Dana", "Scully");
        Bank.getCustomer(0).addAccount(new CheckingAccount(2000));
        Bank.getCustomer(1).addAccount(new SavingsAccount(1000, 3));
        Bank.getCustomer(2).addAccount(new CheckingAccount(1000, 500));
        
        SWINGDemo demo = new SWINGDemo();        
        demo.launchFrame();
    }
}
```

***Резльтат виконання програми:***  

<img src="https://github.com/ppc-ntu-khpi/35-gui-1-Articso/blob/master/images/screen2.png"/>

[![Gitter](https://badges.gitter.im/PPC-SE-2020/OOP.svg)](https://gitter.im/PPC-SE-2020/OOP?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)
![](https://img.shields.io/badge/Made%20with-JAVA-red.svg)
![](https://img.shields.io/badge/Made%20with-%20Netbeans-brightgreen.svg)
![](https://img.shields.io/badge/Made%20at-PPC%20NTU%20%22KhPI%22-blue.svg) 
