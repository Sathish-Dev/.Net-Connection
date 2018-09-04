# .Net-Connection

private void button1_Click(object sender, EventArgs e)
        {
            string connetionString;
            SqlConnection con;
            connetionString = @"Data Source=10.100.8.148;Initial Catalog=training;User ID=training;Password=training";
            con = new SqlConnection(connetionString);
            SqlCommand cmd;
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
