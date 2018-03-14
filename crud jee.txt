
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.util.ArrayList;
import java.util.List;


/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */

/**
 *
 * @author SAMSUNG
 */
public class connectiondb {
    
    
    public static Connection getConnection() throws ClassNotFoundException, SQLException{
         Connection cnx=null;
         Class.forName("mySqlDriver");
         String url="jdbc:mysql://localhost/presonne";
         cnx=DriverManager.getConnection(url, "root","");
         
         return cnx;
    }
    
    public static int save(Etud ed){
        
        int E=0;
        try {
        String sql="INSERT INTO `etudiant`( `nom`, `pwd`, `email`, `pays`) VALUES (?,?,?,?)";
        Connection cnx=connectiondb.getConnection();
        PreparedStatement preparedstatement=cnx.prepareStatement(sql);
        preparedstatement.setString(1, ed.getNom());      
        preparedstatement.setString(2, ed.getEmail());
        preparedstatement.setString(3, ed.getPwd());
        preparedstatement.setString(4, ed.getPays());
        
        E = preparedstatement.executeUpdate();
        cnx.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
        return E;

    }
    
    
    public static int modifier(Etud ed){
        
        int E=0;
        try {
        String sql="UPDATE `etudiant` SET `nom`=?,`pwd`=?,`email`=?,`pays`=? WHERE id=?";
        Connection cnx=connectiondb.getConnection();
        PreparedStatement preparedstatement=cnx.prepareStatement(sql);
        preparedstatement.setString(1, ed.getNom());      
        preparedstatement.setString(2, ed.getEmail());
        preparedstatement.setString(3, ed.getPwd());
        preparedstatement.setString(4, ed.getPays());
        preparedstatement.setInt(5, ed.getId());
        
        E = preparedstatement.executeUpdate();
        cnx.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
        return E;

    }
    
    public static int supprimer(int id){
        
        int E=0;
        try {
        String sql="DELETE FROM `etudiant` WHERE id=?";
        Connection cnx=connectiondb.getConnection();
        PreparedStatement preparedstatement=cnx.prepareStatement(sql);
        
        preparedstatement.setInt(1, id);
        
        E = preparedstatement.executeUpdate();
        cnx.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
        return E;

    }
    
    
     public static Etud afficherId(int id){
        
        Etud E=new Etud();
        try {
        String sql="SELECT * FROM `etudiant` WHERE id=?";
        Connection cnx=connectiondb.getConnection();
        PreparedStatement preparedstatement=cnx.prepareStatement(sql);
        
        preparedstatement.setInt(1, id);
        ResultSet result=preparedstatement.executeQuery();
        
            if (result.next()) {
                E.setId(result.getInt(1));
                E.setNom(result.getString(2));
                E.setEmail(result.getString(3));
                E.setPwd(result.getString(4));
                E.setPays(result.getString(5));
            }
        
        
        
        
        cnx.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
        return E;

    }
     
     public static List<Etud> afficher(){
        
        List<Etud> E=new ArrayList<Etud>();
        try {
        String sql="SELECT * FROM `etudiant`";
        Connection cnx=connectiondb.getConnection();
        PreparedStatement preparedstatement=cnx.prepareStatement(sql);
        
        Etud ET=new Etud();
        ResultSet result=preparedstatement.executeQuery();
        
            if (result.next()) {
                ET.setId(result.getInt(1));
                ET.setNom(result.getString(2));
                ET.setEmail(result.getString(3));
                ET.setPwd(result.getString(4));
                ET.setPays(result.getString(5));
                E.add(ET);
            }
        
        
        
        
        cnx.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
        return E;

    }
   
    
    
}
