  <appSettings>
      <add key="ValidationSettings:UnobtrusiveValidationMode" value="None" />
    </appSettings>

<!DOCTYPE html>

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title></title>
    <style>
         .center {
    margin-left:400px; 
    margin-right:auto;
    margin-top:100px;
    border-width:2px;
  }
        .auto-style1 {
            height: 26px;
        }
        .auto-style2 {
            margin-left: 379px;
            margin-top: 0px;
        }
    </style>
</head>
<body style="background-color:#cee4ea">
    <form id="form1" runat="server">
     <table class ="center">
            <tr>
                <td class="style1" colspan="2">
                    <h1 style="color:blue;"><strong>Registration Details</strong></h1></td>
            </tr>
             <tr>
                <td class="style1" colspan="2">
                    </td>
            </tr>
         <tr>
                <td>
                   Id :</td>
                <td class="style4">
                    <asp:TextBox ID="txtId" runat="server" Text=""></asp:TextBox>
                   
                </td>
            </tr>
            <tr>
                <td class="auto-style1">
                    Name :</td>
                <td class="auto-style1">
                    <asp:TextBox ID="txtname" runat="server" Text=""></asp:TextBox>
                    <asp:RequiredFieldValidator ID="errtxtname" runat="server" controltovalidate="txtname" ErrorMessage="This is a required field." ForeColor="Red"></asp:RequiredFieldValidator>
                            </td>
            </tr>
                       
            <tr>
                <td>
                    Gender :</td>
                <td class="style4">
                    <asp:TextBox ID="txtGender" runat="server" Text=""></asp:TextBox>
                </td>
            </tr>
                   <tr>
                <td>
                    Email ID :</td>
                <td class="style4">
                    <asp:TextBox ID="txtEmail" runat="server" Text=""></asp:TextBox>
                   
                </td>
            </tr>
            <tr>
                <td>
                    Password :</td>
                <td>
                    <asp:TextBox ID="txtPassword" runat="server" Text=""></asp:TextBox>
                                    </td>
            </tr>
         <tr>
           <td><asp:Button ID="btnSubmit" runat="server" Text="Submit" onclick="btnSubmit_Click" />
         </td>
            </tr>
        </table>
        <asp:GridView ID="GridView1" runat="server" AllowPaging="True" AllowSorting="True" AutoGenerateColumns="False" CellPadding="4" CssClass="auto-style2" DataKeyNames="Id" DataSourceID="LinqDataSource1" ForeColor="#333333" GridLines="None" Height="139px" Width="302px">
            <AlternatingRowStyle BackColor="White" ForeColor="#284775" />
            <Columns>
                <asp:CommandField ShowDeleteButton="True" ShowEditButton="True" />
                <asp:BoundField DataField="Id" HeaderText="Id" ReadOnly="True" SortExpression="Id" />
                <asp:BoundField DataField="Name" HeaderText="Name" SortExpression="Name" />
                <asp:BoundField DataField="Email" HeaderText="Email" SortExpression="Email" />
                <asp:BoundField DataField="Password" HeaderText="Password" SortExpression="Password" />
                <asp:BoundField DataField="Gender" HeaderText="Gender" SortExpression="Gender" />
            </Columns>
            <EditRowStyle BackColor="#999999" />
            <FooterStyle BackColor="#5D7B9D" Font-Bold="True" ForeColor="White" />
            <HeaderStyle BackColor="#5D7B9D" Font-Bold="True" ForeColor="White" />
            <PagerStyle BackColor="#284775" ForeColor="White" HorizontalAlign="Center" />
            <RowStyle BackColor="#F7F6F3" ForeColor="#333333" />
            <SelectedRowStyle BackColor="#E2DED6" Font-Bold="True" ForeColor="#333333" />
            <SortedAscendingCellStyle BackColor="#E9E7E2" />
            <SortedAscendingHeaderStyle BackColor="#506C8C" />
            <SortedDescendingCellStyle BackColor="#FFFDF8" />
            <SortedDescendingHeaderStyle BackColor="#6F8DAE" />
        </asp:GridView>
        <asp:LinqDataSource ID="LinqDataSource1" runat="server" ContextTypeName="Linq.LinqqDataContext" EnableDelete="True" EnableUpdate="True" EntityTypeName="" TableName="UserDatas">
        </asp:LinqDataSource>
    </form>
</body>
</html>

Back End


public partial class Registration : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {

        }
        protected void btnSubmit_Click(object sender, EventArgs e)
        {
            LinqqDataContext db = new LinqqDataContext();
            UserData ud = new UserData();
            ud.Id = Convert.ToInt32(txtId.Text);
            ud.Name = txtname.Text;
            ud.Email = txtEmail.Text;
            ud.Password = txtPassword.Text;
            ud.Gender = txtGender.Text;

            db.UserDatas.InsertOnSubmit(ud);
            db.SubmitChanges();
            txtId.Text = "";
            txtname.Text = "";
            txtEmail.Text = "";
            txtPassword.Text = "";
            txtGender.Text = "";
            GridView1.DataBind();

