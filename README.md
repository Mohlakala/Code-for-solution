# Code-for-solution
Source control the code of a solution 
The context of the repository is used to source control the code of a solution 

//
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
using System.Data.SqlClient;


namespace WindowsForm
{
    public partial class Form1 : Form
    {
        //5 global variables;
        SqlConnection conn;
        string connectionString;
        SqlCommand comm;
        SqlDataAdapter adap;
        SqlDataReader dr;
        DataSet ds;

        public Form1()
        {
            InitializeComponent();
        }

        private void btnConnect_Click(object sender, EventArgs e)
        {
            //
            connectionString = @"Data Source = (LocalDB)\MSSQLLocalDB; AttachDbFilename = C:\Users\Student\Desktop\WORKING\WindowsForm\ClientList.mdf; Integrated Security = True";
            conn = new SqlConnection(connectionString);
            conn.Open();
            conn.Close();

            MessageBox.Show("Connected successfully","connection successfully" ,MessageBoxButtons.OK, MessageBoxIcon.Information);

        }

        private void btnDisplay_Click(object sender, EventArgs e)
        {
            //variable declaration
            string sql = "SELECT * FROM Client ";
            //open the connection to the db
            conn.Open();
            //
            adap = new SqlDataAdapter();
            ds = new DataSet();
            //
            comm = new SqlCommand(sql, conn);
            adap.SelectCommand = comm;
            adap.Fill(ds, "SourceTable");
            dataGridView1.DataSource = ds;
            dataGridView1.DataMember = "SourceTable";
            //
            conn.Close();
        }

        private void btnMove_Click(object sender, EventArgs e)
        {
            conn.Open();
            string sql = "SELECT * FROM Client";
            //
            comm = new SqlCommand(sql, conn);
            //
            dr = comm.ExecuteReader();
            //
            while(dr.Read())
            {
                listBox1.Items.Add(dr.GetValue(0) + "\t" + dr.GetValue(1) + "\t" + dr.GetValue(2) + "\t" + dr.GetValue(3));

            }
        }

        private void btnClose_Click(object sender, EventArgs e)
        {
            this.Close();
        }
    }
}
