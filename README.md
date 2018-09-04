# .Net-Connection and CRUD operation

using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Data.SqlClient;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace Sample1
{
    public partial class Form1 : Form
    {
        
        SqlConnection con = new SqlConnection(@"Data Source=10.100.8.148;Initial Catalog=training;User ID=training;Password=training");
        SqlCommand cmd;
        SqlDataAdapter adapt;
        public Form1()
        {
            InitializeComponent();
        }

        private void button1_Click(object sender, EventArgs e)
        {
            
           
            con.Open();
            string s = "insert into gssemp values(@Name,@Emp_id)";
            cmd = new SqlCommand(s, con);
            cmd.Parameters.AddWithValue("@Name", textBox1.Text);
            cmd.Parameters.AddWithValue("@Emp_id", textBox2.Text);
            cmd.CommandType = CommandType.Text;
            int i = cmd.ExecuteNonQuery();
            con.Close();
            MessageBox.Show(i + " Row(s) Inserted ");
            con.Close();
        }

        

        
        private void button2_Click(object sender, EventArgs e)
        {
            if (dataGridView1.ColumnCount > 0)
            {
                con.Open();
                cmd = new SqlCommand("delete from gssemp where Emp_id=@id", con);
                cmd.Parameters.AddWithValue("@id",textBox2.Text);
                cmd.CommandType = CommandType.Text;
                cmd.ExecuteNonQuery();
                con.Close();
                MessageBox.Show("Deleted Successfully...!!!");
            }
        }

        private void button3_Click(object sender, EventArgs e)
        {

            con.Open();
            DataTable dt = new DataTable();
            adapt = new SqlDataAdapter("select * from gssemp", con);
            adapt.Fill(dt);
            dataGridView1.DataSource = dt;
            con.Close();
        }

        private void button4_Click(object sender, EventArgs e)
        {
            con.Open();
            cmd = new SqlCommand("update gssemp set Name=@name where Emp_id=@id", con);            
            cmd.Parameters.AddWithValue("@name", textBox1.Text);
            cmd.Parameters.AddWithValue("@id", textBox2.Text);
            cmd.CommandType = CommandType.Text;
            cmd.ExecuteNonQuery();
            MessageBox.Show("Record Updated Successfully");
            con.Close();
        }
    }
}

