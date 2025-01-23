//
// Source code recreated from a .class file by IntelliJ IDEA
// (powered by FernFlower decompiler)
//

package com.example.demo3;
import com.example.demo3.LoginTela;
import javafx.application.Application;
import javafx.stage.Stage;
public class MainApp extends Application {
    public MainApp() {
    }
    public void start(Stage primaryStage) {
        LoginTela loginTela = new LoginTela(primaryStage);
        loginTela.showLogin();
        primaryStage.setTitle("Sistema de Login Funcional");
        primaryStage.show();
    }

    public static void main(String[] args) {
        launch(args);
    }
}
package com.example.demo3;

import javafx.scene.Node;
import javafx.scene.Scene;
import javafx.scene.control.Alert;
import javafx.scene.control.Button;
import javafx.scene.control.Label;
import javafx.scene.control.PasswordField;
import javafx.scene.control.TextField;
import javafx.scene.control.Alert.AlertType;
import javafx.scene.layout.VBox;
import javafx.stage.Stage;

public class LoginTela {
    private Stage stage;
    private static final String ID_DIRETOR = "diretor";
    private static final String SENHA_DIRETOR = "1234";
    private static final String ID_PROFESSOR = "professor";
    private static final String SENHA_PROFESSOR = "abcd";
    private static final String ID_ALUNO = "aluno";
    private static final String SENHA_ALUNO = "senha123";

    public LoginTela(Stage stage) {
        this.stage = stage;
    }

    public void showLogin() {
        Label lblID = new Label("ID de Registro:");
        TextField txtID = new TextField();
        Label lblSenha = new Label("Senha:");
        PasswordField txtSenha = new PasswordField();
        Button btnLogin = new Button("Login");
        btnLogin.setOnAction((e) -> {
            String id = txtID.getText();
            String senha = txtSenha.getText();
            if (id.equals("diretor") && senha.equals("1234")) {
                this.abrirTelaPrincipal("Diretor");
            } else if (id.equals("professor") && senha.equals("abcd")) {
                this.abrirTelaPrincipal("Professor");
            } else if (id.equals("aluno") && senha.equals("senha123")) {
                this.abrirTelaPrincipal("Aluno");
            } else {
                Alert alert = new Alert(AlertType.ERROR);
                alert.setTitle("Erro de Login");
                alert.setHeaderText("Credenciais inválidas!");
                alert.showAndWait();
            }

        });
        VBox vbox = new VBox((double)10.0F, new Node[]{lblID, txtID, lblSenha, txtSenha, btnLogin});
        Scene scene = new Scene(vbox, (double)300.0F, (double)200.0F);
        this.stage.setScene(scene);
    }

    private void abrirTelaPrincipal(String tipoUsuario) {
        TelaPrincipal telaPrincipal = new TelaPrincipal(tipoUsuario);

       //if por tipo de utilzador
        telaPrincipal.mostrarTela(this.stage);
    }
}


package com.example.demo3;



import javafx.scene.Node;
import javafx.scene.Scene;
import javafx.scene.control.Button;
import javafx.scene.control.Label;
import javafx.scene.layout.VBox;
import javafx.stage.Stage;

public class TelaPrincipal {
    private String tipoUsuario;

    public TelaPrincipal(String tipoUsuario) {
        this.tipoUsuario = tipoUsuario;
    }

    public void mostrarTela(Stage stage) {
        Label lblBoasVindas = new Label("Bem-vindo, " + this.tipoUsuario);
        Button btnFuncionalidade1 = new Button("Funcionalidade 1");
        Button btnFuncionalidade2 = new Button("Funcionalidade 2");
        Button btnFuncionalidade3 = new Button("Funcionalidade 3");
        if ("Diretor".equals(this.tipoUsuario)) {
            btnFuncionalidade1.setDisable(false);
            btnFuncionalidade2.setDisable(false);
            btnFuncionalidade3.setDisable(false);
        } else if ("Professor".equals(this.tipoUsuario)) {
            btnFuncionalidade1.setDisable(false);
            btnFuncionalidade2.setDisable(false);
            btnFuncionalidade3.setDisable(true);
        } else {
            btnFuncionalidade1.setDisable(true);
            btnFuncionalidade2.setDisable(true);
            btnFuncionalidade3.setDisable(true);
        }

        VBox vbox = new VBox((double)10.0F, new Node[]{lblBoasVindas, btnFuncionalidade1, btnFuncionalidade2, btnFuncionalidade3});
        Scene scene = new Scene(vbox, (double)400.0F, (double)300.0F);
        stage.setTitle("Tela Principal - " + this.tipoUsuario);
        stage.setScene(scene);
        stage.show();
    }
}


package com.example.demo3;

import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;
import java.util.Properties;

public class SistemaDeLogin {
    private static final String ARQUIVO_CONFIGURACAO = "config.properties";

    public SistemaDeLogin() {
    }

    public static void salvarConfiguracao(String id, String senha) {
        Properties prop = new Properties();

        try (FileOutputStream out = new FileOutputStream("config.properties")) {
            prop.setProperty("usuario.id", id);
            prop.setProperty("usuario.senha", senha);
            prop.store(out, (String)null);
        } catch (IOException e) {
            e.printStackTrace();
        }

    }

    public static Properties carregarConfiguracao() {
        Properties prop = new Properties();

        try (FileInputStream in = new FileInputStream("config.properties")) {
            prop.load(in);
        } catch (IOException e) {
            e.printStackTrace();
        }

        return prop;
    }
}
