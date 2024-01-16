# C# ve MSSQL'i birbirine bağlayarak 'Microsoft' kullanıcı arayüzü yapma örneği;

1. Adım: Mssql veritabanında 'rehber3' adında database oluşturuyoruz.
2. Adım: Sonra 'kisiler' adında tablo oluşturuyoruz.
3. Adım: Tabloya 'id, ad, soyad, kisiler' kolonları ekliyoruz.
4. Adım: C#'ta 'Microsoft.Data.SqlClient' paketini indiriyoruz.

using Microsoft.Data.SqlClient;   
using Microsoft.Identity.Client;   
using Microsoft.IdentityModel.Tokens;   
using System.CodeDom;    
using System.Data;

namespace rehber3    
{

    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }
        public void ekle()
        { 
            if (yk_ad.Text.IsNullOrEmpty() || yk_soyad.Text.IsNullOrEmpty() || yk_telefon.Text.IsNullOrEmpty())
            {
                MessageBox.Show("Boş Alan Girilemez");
                return;
            }
            var baglanti = "Data Source = \\SQLEXPRESS; Initial Catalog = rehber3; Integrated Security = SSPI; Encrypt=False";
            var sqlbaglanti = new SqlConnection(baglanti);
            try
            {    
                sqlbaglanti.Open();
                var komut = @"insert into kisiler (ad, soyad, telefon) values (@ad, @soyad, @telefon)";
                var sqlkomut = new SqlCommand(komut, sqlbaglanti);
                sqlkomut.Parameters.AddWithValue("@ad", yk_ad.Text);
                sqlkomut.Parameters.AddWithValue("@soyad", yk_soyad.Text);
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
        public void oku()
        {
            var baglanti = "Data Source = \\SQLEXPRESS; Initial Catalog = rehber3; Integrated Security = SSPI; Encrypt=False";
            var sqlbaglanti = new SqlConnection(baglanti);
            try
            {
                sqlbaglanti.Open();
                var komut = @"Select * From kisiler order by ad";
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
        int id = 0;
        public void güncelle()
        {
            var baglanti = "Data Source = \\SQLEXPRESS; Initial Catalog = rehber3; Integrated Security = SSPI; Encrypt=False";
            var sqlbaglanti = new SqlConnection(baglanti);
            try
            {
                sqlbaglanti.Open();
                var komut = @"Update kisiler SET ad = @ad, soyad = @soyad, telefon = @telefon WHERE id = @id";
                var sqlkomut = new SqlCommand(komut, sqlbaglanti);
                sqlkomut.Parameters.AddWithValue("@ad", yk_ad.Text);
                sqlkomut.Parameters.AddWithValue("@soyad", yk_soyad.Text);
                sqlkomut.Parameters.AddWithValue("@telefon", yk_telefon.Text);
                sqlkomut.Parameters.AddWithValue("@id", id);
                ; sqlkomut.ExecuteNonQuery();
                oku();
            }
            catch (Exception ex)
            {
                MessageBox.Show(ex.Message);
            }
            finally
            {
                sqlbaglanti.Close();
                id = 0;
            }
        }
        public void sil()
        {
            var baglanti = "Data Source = \\SQLEXPRESS; Initial Catalog = rehber3; Integrated Security = SSPI; Encrypt=False";
            var sqlbaglanti = new SqlConnection(baglanti);
            try
            {
                sqlbaglanti.Open();
                var komut = @"Delete From kisiler where id = @id";
                var sqlkomut = new SqlCommand(komut, sqlbaglanti);
                sqlkomut.Parameters.AddWithValue("@id", id);
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
                id = 0;
            }
        }
        public void temizle()
        {
            yk_ad.Clear();
            yk_soyad.Clear();
            yk_telefon.Clear();
        }
        private void d_ekle_Click(object sender, EventArgs e)
        {
            ekle();
        }

        private void Form1_Load(object sender, EventArgs e)
        {
            oku();
        }

        private void tablo_liste_CellContentDoubleClick(object sender, DataGridViewCellEventArgs e)
        {
            yk_ad.Text = tablo_liste[gb_ad.Name, tablo_liste.CurrentCell.RowIndex].Value.ToString();
            yk_soyad.Text = tablo_liste[gb_soyad.Name, tablo_liste.CurrentCell.RowIndex].Value.ToString();
            yk_telefon.Text = tablo_liste[gb_telefon.Name, tablo_liste.CurrentCell.RowIndex].Value.ToString();
            id = Convert.ToInt32(tablo_liste[gb_id.Name, tablo_liste.CurrentCell.RowIndex].Value);
        }

        private void d_güncelle_Click(object sender, EventArgs e)
        {
            güncelle();
        }

        private void d_sil_Click(object sender, EventArgs e)
        {
            sil();
        }

        private void pictureBox1_Click(object sender, EventArgs e)
        {
            pictureBox1.Image = Image.FromFile("resim.jpg");
        }
    }
}
