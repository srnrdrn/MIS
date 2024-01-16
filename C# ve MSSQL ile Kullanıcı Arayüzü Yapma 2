1. Adım: MSSQL veritabanında rehber2 adında database oluşturuyoruz
2. Adım: rehber2'de 'kisiler' adında tablo oluşturuyoruz.
3. Adım: Tablomuza 'id, adi, soyadi, dtarih, adres, telefon' kolonları ekliyoruz.
4. Adım: MSSQL'i C#'a bağlıyoruz.

using Microsoft.Data.SqlClient;  
using Microsoft.IdentityModel.Tokens;  
using System.Data;  
using System.Data.Common;  
using System.Data.SqlClient;  
using static System.Runtime.InteropServices.JavaScript.JSType;

namespace rehber2  
{

    public partial class Form1 : Form
    {
        int ID = 0;
        public void duzelt()
        {
            var baglanti = @"Data Source = \SQLEXPRESS; Initial Catalog = rehber2; Integrated Security = SSPI; Encrypt=False";
            var sqlbaglanti = new SqlConnection(baglanti);
            try
            {
                sqlbaglanti.Open();
                var komut = @"Update kisiler SET adi = @adi, soyadi = @soyadi WHERE ID = @ID";
                var sqlkomut = new SqlCommand(komut, sqlbaglanti);
                sqlkomut.Parameters.AddWithValue("@adi", yk_adi.Text);
                sqlkomut.Parameters.AddWithValue("@soyadi", yk_soyadi.Text);
                sqlkomut.Parameters.AddWithValue("@dtarih", tk_dtarih.Text);
                sqlkomut.Parameters.AddWithValue("@adres", yk_adres.Text);
                sqlkomut.Parameters.AddWithValue("@telefon", yk_telefon.Text);
                sqlkomut.Parameters.AddWithValue("@ID", ID);
                ; sqlkomut.ExecuteNonQuery();
            }
            catch (Exception ex)
            {
                MessageBox.Show(ex.Message);
            }
            finally
            {
                sqlbaglanti.Close();
                ID = 0;
            }
        }
        public void sil()
        {
            var baglanti = @"Data Source = \SQLEXPRESS; Initial Catalog = rehber2; Integrated Security = SSPI; Encrypt=False";
            var sqlbaglanti = new SqlConnection(baglanti);
            try
            {
                sqlbaglanti.Open();
                var komut = @"Delete from kisiler Where ID = @ID";
                var sqlkomut = new SqlCommand(komut, sqlbaglanti);
                sqlkomut.Parameters.AddWithValue("@ID", ID);
                ; sqlkomut.ExecuteNonQuery();

                MessageBox.Show("kayıt silindi");
                oku();
                temizle();
            }
            catch (Exception ex)
            {
                MessageBox.Show(ex.Message);
            }
            finally
            {
                sqlbaglanti.Close();
                ID = 0;
            }
        }
        public void temizle()
        {
            yk_adi.Clear();
            yk_soyadi.Clear();
            tk_dtarih.CustomFormat = " ";
            tk_dtarih.Format = DateTimePickerFormat.Custom;
            yk_adres.Clear();
            yk_telefon.Clear();

        }
        public void oku()
        {
            var baglanti = @"Data Source = \SQLEXPRESS; Initial Catalog = rehber2; Integrated Security = SSPI; Encrypt=False";
            var sqlbaglanti = new SqlConnection(baglanti);
            try
            {
                sqlbaglanti.Open();
                var komut = @"Select * From kisiler order by adi";
                var sqlkomut = new SqlCommand(komut, sqlbaglanti);
                var Adapter = new SqlDataAdapter(sqlkomut);
                var ds = new DataSet();
                Adapter.Fill(ds);
                tablo_liste.DataSource = ds.Tables[0];
            }
            catch (Exception ex)
            {
                MessageBox.Show(ex.Message);
            }
            finally { sqlbaglanti.Close(); }
        }
        public Form1()
        {
            InitializeComponent();
        }
        public void kaydet()
        {
            if (yk_adi.Text.IsNullOrEmpty() || yk_soyadi.Text.IsNullOrEmpty() || yk_adres.Text.IsNullOrEmpty() || yk_telefon.Text.IsNullOrEmpty())
            {

                MessageBox.Show("Boş Alan Girilemez");
                return;
            }

            try
            {
                var gg = tk_dtarih.Text;
            }
            catch
            {
                MessageBox.Show("Boş Alan Girilemez");
                return;
            }

            var baglanti = "Data Source = \\SQLEXPRESS; Initial Catalog = rehber2; Integrated Security = SSPI; Encrypt=False";
            var sqlbaglanti = new SqlConnection(baglanti);
            try
            {
                sqlbaglanti.Open();
                var komut = @"insert into kisiler (adi, soyadi, dtarih, adres, telefon) values (@adi, @soyadi, @dtarih, @adres, @telefon)";
                var sqlkomut = new SqlCommand(komut, sqlbaglanti);
                sqlkomut.Parameters.AddWithValue("@adi", yk_adi.Text);
                sqlkomut.Parameters.AddWithValue("@soyadi", yk_soyadi.Text);
                sqlkomut.Parameters.AddWithValue("@dtarih", tk_dtarih.Value);
                sqlkomut.Parameters.AddWithValue("@adres", yk_adres.Text);
                sqlkomut.Parameters.AddWithValue("@telefon", yk_telefon.Text);
                ; sqlkomut.ExecuteNonQuery();

                MessageBox.Show("kayıt tamamlandı");
            }
            catch (Exception ex)
            {
                MessageBox.Show(ex.Message);
            }
            finally { sqlbaglanti.Close(); }

        }

        private void d_kaydet_Click(object sender, EventArgs e)
        {

            kaydet();
        }

        private void Form1_Load(object sender, EventArgs e)
        {
            oku();
            tk_dtarih.CustomFormat = " ";
            tk_dtarih.Format = DateTimePickerFormat.Custom;
        }

        private void tk_dtarih_ValueChanged(object sender, EventArgs e)
        {
            tk_dtarih.CustomFormat = "dd.MM.yyyy";
            tk_dtarih.Format = DateTimePickerFormat.Custom;
        }

        private void yk_adi_TextChanged(object sender, EventArgs e)
        {

        }

        private void tablo_liste_CellContentDoubleClick(object sender, DataGridViewCellEventArgs e)
        {

        }

        private void button1_Click(object sender, EventArgs e)
        {
            duzelt();
        }

        private void tablo_liste_DoubleClick(object sender, EventArgs e)
        {
            tk_dtarih.CustomFormat = "dd.MM.yyyy";
            tk_dtarih.Format = DateTimePickerFormat.Custom;
            yk_adi.Text = tablo_liste[gb_adi.Name, tablo_liste.CurrentCell.RowIndex].Value.ToString();
            yk_soyadi.Text = tablo_liste[gb_soyadi.Name, tablo_liste.CurrentCell.RowIndex].Value.ToString();
            tk_dtarih.Text = tablo_liste[gb_dtarih.Name, tablo_liste.CurrentCell.RowIndex].Value.ToString();
            yk_adres.Text = tablo_liste[gb_adres.Name, tablo_liste.CurrentCell.RowIndex].Value.ToString();
            yk_telefon.Text = tablo_liste[gb_telefon.Name, tablo_liste.CurrentCell.RowIndex].Value.ToString();
            ID = Convert.ToInt32(tablo_liste[gb_ID.Name, tablo_liste.CurrentCell.RowIndex].Value);
        }

        private void d_sil_Click(object sender, EventArgs e)
        {
            sil();
        }
    }
}
