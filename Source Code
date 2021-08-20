package sample;

//IMPORTING THE NECESSARY HEADER FILES
import javafx.application.Application;
import javafx.event.ActionEvent;
import javafx.event.EventHandler;
import javafx.geometry.Insets;
import javafx.scene.Scene;
import javafx.scene.control.*;
import javafx.scene.paint.Color;
import javafx.scene.text.Font;
import javafx.stage.Stage;
import javafx.scene.layout.*;
import javafx.beans.property.BooleanProperty;
import javafx.beans.property.SimpleBooleanProperty;
import java.lang.Math;
import java.sql.*;

public class Main extends Application {
    @Override
    public void start(Stage primaryStage) {
            final BooleanProperty firstTime = new SimpleBooleanProperty(true);
            Font font = Font.font("Franklin Gothic", 26);
            
            // RANDOM NUMBER GENERATOR FOR OTP
            int min = 100000;
            int max = 999999;
            int random_number;
            random_number = (int)(Math.random() * (max - min + 1) + min);
            Label email_label = new Label("Email ID: ");
            Label pass_label = new Label("Password: ");
            
            // EMAIL TEXT FIELD
            TextField email = new TextField();
            email.setPromptText("abc@gmail.com");
            email.setMinSize(50, 25);
            email_label.setFont(font);
            
            // PASSWORD FIELD
            PasswordField pass = new PasswordField();
            pass.setPromptText("qwerty");
            pass.setMinSize(50, 25);
            pass_label.setFont(font);
            
            // AUTHENTICATION LABEL
            Label valid_label = new Label("");
            Button finish_btn = new Button("Finish");
            finish_btn.setMinSize(50, 20);
            finish_btn.setFont(Font.font("Franklin Gothic", 20));
            finish_btn.setVisible(false);
            Label line_break = new Label("\n");
            
            // BUTTON TO MOVE TO THE NEXT WINDOW
            Button next_btn = new Button("Next ->");
            next_btn.setMinSize(50, 20);
            next_btn.setFont(Font.font("Franklin Gothic", 20));
            
            // EVENT HANDLER ATTACHED TO THE NEXT BUTTON
            next_btn.setOnAction(new EventHandler < ActionEvent > () {
                        @Override
                        public void handle(ActionEvent actionEvent) {
                            System.out.println("Email ID Entered: " + email.getText());
                            System.out.println("Password Entered: " + pass.getText());

                            boolean flag = false;
                            try {
                                Class.forName("com.mysql.cj.jdbc.Driver");
                                Connection con =
                                    DriverManager.getConnection("jdbc:mysql://localhost:3306/19bds0019",
                                        "root", "");
                                Statement stmt1 = con.createStatement();
                                ResultSet rs = stmt1.executeQuery("select * from details");
                                
                                while (rs.next()) {
                                    if (rs.getString(1).equals(email.getText()) &&
                                        rs.getString(2).equals(pass.getText())) {
                                        flag = true;
                                        valid_label.setText("Successfully Logged In!");
                                        valid_label.setFont(font);
                                        valid_label.setTextFill(Color.web("#008000"));
                                        
                                        if (valid_label.getText().equals("Successfully Logged
                                                In!")){
                                                System.out.println("User Found in the Database! Login
                                                    Successful!");
                                                }
                                            }
                                            else if (rs.getString(1).equals(email.getText()) &&
                                                (!rs.getString(2).equals(pass.getText()))) {
                                                flag = true;
                                                valid_label.setText("Incorrect Password!!");
                                                valid_label.setFont(font);
                                                valid_label.setTextFill(Color.web("#ff0000"));
                                            }
                                        }
                                        con.close();
                                    } catch (Exception e) {
                                        e.printStackTrace();
                                    }
                                    if (flag) {
                                        try {
                                            Thread.sleep(1000);
                                        } catch (InterruptedException e) {
                                            e.printStackTrace();
                                        }
                                    } else {
                                        final BooleanProperty firstTime = new SimpleBooleanProperty(true);
                                        Label otp = new Label("OTP: " + random_number);
                                        otp.setFont(font);
                                        Label otp_label = new Label("Enter the above OTP: ");
                                        otp_label.setFont(font);
                                        TextField otp_entered = new TextField();
                                        otp_entered.setPromptText("******");
                                        otp_entered.setMinSize(50, 25);
                                        Button verify_btn = new Button("Verify OTP");
                                        verify_btn.setFont(Font.font("Franklin Gothic", 20));
                                        Label error_label = new Label("");
                                        
                                        // GENERATING NEW STAGE AND LAYOUT
                                        VBox second_layout = new VBox();
                                        Stage second_stage = new Stage();
                                        
                                        // EVENT HANDLER TO VERIFY THE OTP
                                        verify_btn.setOnAction(new EventHandler < ActionEvent > () {
                                                @Override
                                                public void handle(ActionEvent actionEvent) {
                                                    int otp_entered_num = 0;
                                                    System.out.println("OTP Entered: " +
                                                        otp_entered.getText());
                                                    if (!otp_entered.getText().equals("")) {
                                                        otp_entered_num =
                                                            Integer.parseInt(otp_entered.getText());
                                                    }
                                                    if (otp_entered_num == random_number) {
                                                        try {
                                                            Class.forName("com.mysql.cj.jdbc.Driver");
                                                            Connection con =
                                                                DriverManager.getConnection("jdbc:mysql://localhost:3306/19bds0019",
                                                                    "root", "");
                                                                    
                                                            // INSERTING VALUES INTO THE DATABASE
                                                            PreparedStatement stmt =
                                                                con.prepareStatement("insert into details values(?,?)");
                                                            stmt.setString(1, email.getText());
                                                            stmt.setString(2, pass.getText());
                                                            int i = stmt.executeUpdate();
                                                            System.out.println(i + " record inserted");
                                                            System.out.println("OTP Verified!");
                                                            con.close();
                                                            System.out.println("\nOTP VERIFICATION
                                                                SUCCESSFUL!");
                                                                second_stage.close(); valid_label.setText("OTP Matched!\nSuccessfully
                                                                    Saved into the Database!");
                                                                    valid_label.setFont(font); valid_label.setTextFill(Color.web("#008000"));
                                                                }
                                                                catch (Exception e) {
                                                                    e.printStackTrace();
                                                                }
                                                            }
                                                            else {
                                                                System.out.println("Invalid OTP Entered! Try Again!");
                                                                error_label.setText("Error! Please Try Again!");
                                                                error_label.setFont(font);
                                                                error_label.setTextFill(Color.web("#ff0000"));
                                                            }
                                                        }
                                                    });

                                                // ADDING NODES TO THE SECOND LAYOUT
                                                second_layout.getChildren().addAll(otp, otp_label, otp_entered,
                                                    verify_btn, error_label);
                                                second_layout.setPadding(new Insets(20));
                                                second_layout.setSpacing(20);
                                                Scene second_scene = new Scene(second_layout, 600, 400);
                                                second_stage.setScene(second_scene);
                                                second_stage.setTitle("Authentication Required");
                                                second_stage.setX(primaryStage.getX() + 40);
                                                second_stage.setY(primaryStage.getY() + 40);
                                                second_stage.show();
                                                otp_entered.focusedProperty().addListener((observable, oldValue,
                                                    newValue) - > {
                                                    if (newValue && firstTime.get()) {
                                                        second_layout.requestFocus();
                                                        firstTime.setValue(false);
                                                    }
                                                });
                                            }
                                        }
                                    });
                                    
                                //ADDING NODES TO THE INITIAL LAYOUT
                                VBox root = new VBox();
                                root.getChildren().addAll(email_label, email, pass_label, pass, line_break, next_btn, valid_l abel, finish_btn);
                                root.setSpacing(10);
                                root.setPadding(new Insets(20));
                                primaryStage.setScene(new Scene(root, 600, 400));
                                primaryStage.setTitle("OTP Login Verification System");
                                System.out.println("PROGRAM INITIATED..");
                                primaryStage.show();
                                
                                //FUNCTION TO REMOVE THE AUTO-FOCUS ON THE TEXT FIELDS
                                email.focusedProperty().addListener((observable, oldValue, newValue) - > {
                                    if (newValue && firstTime.get()) {
                                        root.requestFocus();
                                        firstTime.setValue(false);
                                    }
                                });
                            }
                            
                            // LAUNCHING THE APPLICATION
                            public static void main(String[] args) {
                                launch(args);
                            }
                        }
