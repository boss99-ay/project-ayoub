# project-ayoub
programme de Validation avancée in asp.net
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="Default.aspx.cs" Inherits="Validation_avancée._Default" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head id="Head1" runat="server">
<meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>
    <title></title>
    <script type="text/javascript">
        function PassIdentifiantValidation(source, args) {
            var identifiant = document.getElementById("TextBox1").value;
            var pass = args.Value;            
            if (identifiant && pass.indexOf(identifiant) != -1) {
                args.IsValid = false;
            }
            else {
                args.IsValid = true;
            }
        }
    </script>
</head>
<body>
    <form id="form1" runat="server">
    <h3>Formulaire de saisie du mot de passe</h3>
        <div>
             <asp:Label ID="Label1" runat="server" Text="Identifiant" Width="180px"></asp:Label>
            &nbsp;
            <br />
            <asp:TextBox ID="TextBox1" runat="server"></asp:TextBox>
             &nbsp;
            <asp:RequiredFieldValidator ID="RequiredFieldValidator1"
                runat="server" ControlToValidate="TextBox1" Display="Dynamic"
                ErrorMessage="L'identifiant est obligatoire."
                ForeColor="Red" Text="*" />&nbsp;&nbsp;
            <br />
            <br />
            <asp:Label ID="Label2" runat="server" Text="Mot de passe" Width="180px"></asp:Label>
            &nbsp;
            <br />
            <asp:TextBox ID="TextBox2" runat="server" TextMode="Password"></asp:TextBox>
             &nbsp;                
            <asp:RequiredFieldValidator ID="RequiredFieldValidator2"
                runat="server" ControlToValidate="TextBox2" Display="Dynamic"
                ErrorMessage="Le mot de passe est obligatoire."
                ForeColor="Red" Text="*" />&nbsp;&nbsp; 
            <asp:RegularExpressionValidator ID="RegularExpressionValidator1" runat="server"
                ControlToValidate="TextBox2"
                ErrorMessage="Le mot de passe doit comporter au moins 8 caractères."
                ForeColor="Red" Text="*" Display="Dynamic"
                ValidationExpression=".{8,}"  />&nbsp;&nbsp;             
            <asp:RegularExpressionValidator ID="RegularExpressionValidator2"
                runat="server" ControlToValidate="TextBox2" Display="Dynamic"
                ErrorMessage="Le mot de passe doit contenir au moins une lettre MAJUSCULE."
                ForeColor="Red" Text="*"
                ValidationExpression=".*[A-Z].*" />&nbsp;&nbsp;
             <asp:RegularExpressionValidator ID="RegularExpressionValidator3"
                runat="server" ControlToValidate="TextBox2" Display="Dynamic"
                ErrorMessage="Le mot de passe doit contenir au moins une lettre minuscule."
                ForeColor="Red" Text="*"
                ValidationExpression=".*[a-z].*" />&nbsp;&nbsp;
             <asp:RegularExpressionValidator ID="RegularExpressionValidator4"
                runat="server" ControlToValidate="TextBox2" Display="Dynamic"
                ErrorMessage="Le mot de passe doit contenir au moins un chiffre."
                ForeColor="Red" Text="*"
                ValidationExpression=".*[0-9].*" />&nbsp;&nbsp;
            <asp:RegularExpressionValidator ID="RegularExpressionValidator5" runat="server"
                ControlToValidate="TextBox2"
                ErrorMessage="Le mot de passe doit contenir au moins un caractères spécial (@ # & % ! = ? + - * /)."
                ForeColor="Red" Text="*" Display="Dynamic"
                ValidationExpression=".*[@#&%!=?+*-/].*"  />&nbsp;&nbsp;              
             <asp:CustomValidator ID="CustomValidator1" runat="server"
                ControlToValidate="TextBox2"
                ErrorMessage="Le mot de passe ne peut pas contenir l'identifiant."
                ForeColor="Red" Text="*" Display="Dynamic"
                ClientValidationFunction="PassIdentifiantValidation"/>&nbsp;&nbsp;     
            <br />
            <br />
            <asp:Label ID="Label3" runat="server" Text="Confirmer le mot de passe"></asp:Label>
            &nbsp; 
            <br />
            <asp:TextBox ID="TextBox3" runat="server" TextMode="Password" ></asp:TextBox>&nbsp;&nbsp;           
            <asp:RequiredFieldValidator ID="RequiredFieldValidator3"
                runat="server" ControlToValidate="TextBox3" Display="Dynamic"
                ErrorMessage="La confirmation du mot de passe est obligatoire."
                ForeColor="Red" Text="*" />&nbsp;&nbsp;  
            <asp:CompareValidator ID="CompareValidator1" runat="server"
                ControlToCompare="TextBox2" ControlToValidate="TextBox3" 
                ErrorMessage="Les deux mots de passe ne sont pas identiques"
                ForeColor="Red" Text="*" />
            <br />
        </div>
        <div>
            <br />
            <asp:Button ID="Button1" runat="server" Text="Valider" OnClick="Button1_Click" />
            <br />
            <br />
            <asp:Label ID="lblMsg" runat="server" ForeColor="Green"></asp:Label>
            <br />
        </div>
        <div>
            <asp:ValidationSummary ID="ValidationSummary1" runat="server" ForeColor="Red"
                HeaderText="Veuillez corriger les erreurs suivantes:" />
            <br />
        </div>
    </form>
</body>
</html>
--------code c#-----
using System;
using System.Collections;
using System.Configuration;
using System.Data;
using System.Linq;
using System.Web;
using System.Web.Security;
using System.Web.UI;
using System.Web.UI.HtmlControls;
using System.Web.UI.WebControls;
using System.Web.UI.WebControls.WebParts;
using System.Xml.Linq;

namespace Validation_avancée
{
    public partial class _Default : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {

        }

        protected void Button1_Click(object sender, EventArgs e)
        {
            if (Page.IsValid)
            {
                lblMsg.Text = "Les données saisies sont valides. Merci!";
            }
            
        
        }
    }
}
