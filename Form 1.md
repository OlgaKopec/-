# -
Приложения для оценки влияния дивидендной политики на капитализацию компаний

using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Data.SqlClient;
using System.Drawing;
using System.IO;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace WindowsFormsApp7
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
            
    }
       public bool UpdateInForm = false;
        int a = 2009;
        int z = 0;
        private void button1_Click(object sender, EventArgs e)
        {
            dataGridView1.RowCount = 10;

            double AD = Convert.ToDouble(textBox1.Text);
            double N = Convert.ToDouble(textBox3.Text);
            double Po = Convert.ToDouble(textBox4.Text);
            double Pp = Convert.ToDouble(textBox5.Text);
            double No = Convert.ToDouble(textBox6.Text);
            double Np = Convert.ToDouble(textBox7.Text);
            double x = AD * N;
            double y = (No * Po) + (Np * Pp);
            UpdateInForm = true;

            this.dataGridView1.Rows[0 + z].Cells[0].Value = a;
                    this.dataGridView1.Rows[0 + z].Cells[1].Value = x;   
                    this.dataGridView1.Rows[0 + z].Cells[2].Value = y;
                    z = z+1;
                    a = a+1;
            chart1.Series[1].Points.AddXY(a, x);
            chart1.Series[0].Points.AddXY(a, y);
            chart1.ChartAreas[0].AxisX.MajorGrid.Enabled = false;
            chart1.ChartAreas[0].AxisY.MajorGrid.Enabled = false;
            UpdateInForm = true;
        }
        private void button2_Click(object sender, EventArgs e)
        {
            textBox1.Clear();
            textBox3.Clear();
            textBox4.Clear();
            textBox5.Clear();
            textBox6.Clear();
            textBox7.Clear();
        }
        private void textBox7_KeyPress_1(object sender, KeyPressEventArgs e)
        {
            {
                char number = e.KeyChar;
                if (!Char.IsDigit(number) && number != 44 && number != 8)
                {
                    e.Handled = true;
                }
            }
        }
        private void textBox7_TextChanged(object sender, EventArgs e)
        {
            UpdateInForm = true;
        }
        private void сохранитьToolStripMenuItem_Click(object sender, EventArgs e)
        {
            Stream myStream;
            saveFileDialog1.Filter = "txt files (*.txt)|*.txt|All files (*.*)|*.*";
            saveFileDialog1.FilterIndex = 3;
            saveFileDialog1.RestoreDirectory = true;
            if (saveFileDialog1.ShowDialog() == DialogResult.OK)
            {
                if ((myStream = saveFileDialog1.OpenFile()) != null)
                {
                    StreamWriter myWritet = new StreamWriter(myStream);
                    try
                    {
                        for (int i = 0; i < dataGridView1.RowCount; i++)
                        {
                            for (int j = 0; j < dataGridView1.ColumnCount; j++)
                            {
                                myWritet.Write(dataGridView1.Rows[i].Cells[j].Value.ToString() + " ");
                            }
                            myWritet.WriteLine();
                        }
                    }
                    catch (Exception ex)
                    {
                        //MessageBox.Show(ex.Message);
                    }
                    finally
                    {
                        myWritet.Close();
                    }
                }
            }
        }

        private void оПрограммеToolStripMenuItem1_Click(object sender, EventArgs e)
        {
            Form2 f2 = new Form2();
            f2.ShowDialog();
        }

        private void справкаToolStripMenuItem1_Click(object sender, EventArgs e)
        {
            Form3 f3 = new Form3();
            f3.ShowDialog();
        }
    }
        }
