nguyen xuan an 24810310247
# BÁO CÁO BÀI TẬP LẬP TRÌNH WINDOWS FORMS (C#)

## THÔNG TIN SINH VIÊN
- **Họ và tên:** nguyễn xuân an
- **MSSV:** 24810310247
- **Lớp:** d19cnpm3
---
bai 1 
Form1.Designer.cs
using System.ComponentModel;
using System.Windows.Forms;

namespace WindowsFormsApp1
{
    partial class Form1
    {
        private IContainer components = null;

        protected override void Dispose(bool disposing)
        {
            if (disposing && (components != null))
            {
                components.Dispose();
            }
            base.Dispose(disposing);
        }

        #region Windows Form Designer generated code
        private void InitializeComponent()
        {
            this.components = new Container();
            this.AutoScaleMode = AutoScaleMode.Font;
            this.ClientSize = new System.Drawing.Size(520, 480);
            this.Text = "Form Đăng Ký Tài Khoản";
        }
        #endregion
    }
}
Form1.cs
using System;
using System.Drawing;
using System.Windows.Forms;

namespace WindowsFormsApp1
{
    public partial class Form1 : Form
    {
        // Controls Nhóm thông tin cá nhân
        private TextBox txtTenDangNhap, txtMatKhau, txtXacNhanMatKhau;

        // Controls Nhóm thông tin bổ sung
        private DateTimePicker dtpNgaySinh;
        private RadioButton rdbNam, rdbNu;
        private CheckBox chkDieuKhoan;

        // Buttons & ErrorProvider
        private Button btnDangKy, btnLamMoi;
        private ErrorProvider epCheck;

        public Form1()
        {
            InitializeComponent();
            InitializeComponentsCustom();
        }

        private void InitializeComponentsCustom()
        {
            this.StartPosition = FormStartPosition.CenterScreen;
            this.FormBorderStyle = FormBorderStyle.FixedSingle;
            this.MaximizeBox = false;

            // Khởi tạo ErrorProvider không nhấp nháy
            epCheck = new ErrorProvider { BlinkStyle = ErrorBlinkStyle.NeverBlink };

            // Bố cục chính
            TableLayoutPanel mainLayout = new TableLayoutPanel
            {
                Dock = DockStyle.Fill,
                RowCount = 3,
                ColumnCount = 1,
                Padding = new Padding(15)
            };
            mainLayout.RowStyles.Add(new RowStyle(SizeType.Absolute, 175F)); // Thông tin cá nhân
            mainLayout.RowStyles.Add(new RowStyle(SizeType.Absolute, 175F)); // Thông tin bổ sung
            mainLayout.RowStyles.Add(new RowStyle(SizeType.Percent, 100F));  // Buttons

            // --- 1. NHÓM THÔNG TIN CÁ NHÂN ---
            GroupBox gbCaNhan = new GroupBox { Text = "Thông tin cá nhân", Dock = DockStyle.Fill };
            TableLayoutPanel pnlCaNhan = new TableLayoutPanel
            {
                Dock = DockStyle.Fill,
                ColumnCount = 2,
                RowCount = 3,
                Padding = new Padding(10)
            };
            pnlCaNhan.ColumnStyles.Add(new ColumnStyle(SizeType.Percent, 35F));
            pnlCaNhan.ColumnStyles.Add(new ColumnStyle(SizeType.Percent, 65F));

            txtTenDangNhap = new TextBox { Anchor = AnchorStyles.Left | AnchorStyles.Right };
            txtMatKhau = new TextBox { Anchor = AnchorStyles.Left | AnchorStyles.Right, UseSystemPasswordChar = true };
            txtXacNhanMatKhau = new TextBox { Anchor = AnchorStyles.Left | AnchorStyles.Right, UseSystemPasswordChar = true };

            pnlCaNhan.Controls.Add(new Label { Text = "Tên đăng nhập:", Anchor = AnchorStyles.Left, AutoSize = true }, 0, 0);
            pnlCaNhan.Controls.Add(txtTenDangNhap, 1, 0);
            pnlCaNhan.Controls.Add(new Label { Text = "Mật khẩu:", Anchor = AnchorStyles.Left, AutoSize = true }, 0, 1);
            pnlCaNhan.Controls.Add(txtMatKhau, 1, 1);
            pnlCaNhan.Controls.Add(new Label { Text = "Xác nhận mật khẩu:", Anchor = AnchorStyles.Left, AutoSize = true }, 0, 2);
            pnlCaNhan.Controls.Add(txtXacNhanMatKhau, 1, 2);

            gbCaNhan.Controls.Add(pnlCaNhan);

            // --- 2. NHÓM THÔNG TIN BỔ SUNG ---
            GroupBox gbBoSung = new GroupBox { Text = "Thông tin bổ sung", Dock = DockStyle.Fill };
            TableLayoutPanel pnlBoSung = new TableLayoutPanel
            {
                Dock = DockStyle.Fill,
                ColumnCount = 2,
                RowCount = 3,
                Padding = new Padding(10)
            };
            pnlBoSung.ColumnStyles.Add(new ColumnStyle(SizeType.Percent, 35F));
            pnlBoSung.ColumnStyles.Add(new ColumnStyle(SizeType.Percent, 65F));

            dtpNgaySinh = new DateTimePicker
            {
                Anchor = AnchorStyles.Left | AnchorStyles.Right,
                Format = DateTimePickerFormat.Custom,
                CustomFormat = "dd/MM/yyyy"
            };

            FlowLayoutPanel pnlGioiTinh = new FlowLayoutPanel { Dock = DockStyle.Fill, FlowDirection = FlowDirection.LeftToRight };
            rdbNam = new RadioButton { Text = "Nam", Checked = true, AutoSize = true };
            rdbNu = new RadioButton { Text = "Nữ", AutoSize = true, Margin = new Padding(20, 0, 0, 0) };
            pnlGioiTinh.Controls.AddRange(new Control[] { rdbNam, rdbNu });

            chkDieuKhoan = new CheckBox { Text = "Đồng ý với Điều khoản dịch vụ", AutoSize = true, Anchor = AnchorStyles.Left };

            pnlBoSung.Controls.Add(new Label { Text = "Ngày sinh:", Anchor = AnchorStyles.Left, AutoSize = true }, 0, 0);
            pnlBoSung.Controls.Add(dtpNgaySinh, 1, 0);
            pnlBoSung.Controls.Add(new Label { Text = "Giới tính:", Anchor = AnchorStyles.Left, AutoSize = true }, 0, 1);
            pnlBoSung.Controls.Add(pnlGioiTinh, 1, 1);
            pnlBoSung.Controls.Add(chkDieuKhoan, 1, 2);

            gbBoSung.Controls.Add(pnlBoSung);

            // --- 3. NÚT ĐĂNG KÝ VÀ LÀM MỚI ---
            FlowLayoutPanel pnlButtons = new FlowLayoutPanel
            {
                Dock = DockStyle.Fill,
                FlowDirection = FlowDirection.RightToLeft,
                Margin = new Padding(0, 10, 0, 0)
            };
            btnDangKy = new Button { Text = "Đăng Ký", Width = 100, Height = 35 };
            btnLamMoi = new Button { Text = "Làm Mới", Width = 100, Height = 35, Margin = new Padding(0, 0, 10, 0) };

            btnDangKy.Click += BtnDangKy_Click;
            btnLamMoi.Click += BtnLamMoi_Click;

            pnlButtons.Controls.AddRange(new Control[] { btnDangKy, btnLamMoi });

            // Nối giao diện
            mainLayout.Controls.Add(gbCaNhan, 0, 0);
            mainLayout.Controls.Add(gbBoSung, 0, 1);
            mainLayout.Controls.Add(pnlButtons, 0, 2);

            this.Controls.Add(mainLayout);
        }

        // --- BẮT LỖI GIAO DIỆN KHI NHẤN NÚT ĐĂNG KÝ ---
        private void BtnDangKy_Click(object sender, EventArgs e)
        {
            epCheck.Clear();
            bool isValid = true;

            // 1. Kiểm tra Tên đăng nhập không được để trống
            if (string.IsNullOrWhiteSpace(txtTenDangNhap.Text))
            {
                epCheck.SetError(txtTenDangNhap, "Tên đăng nhập không được để trống!");
                isValid = false;
            }

            // 2. Kiểm tra Mật khẩu không được để trống
            if (string.IsNullOrWhiteSpace(txtMatKhau.Text))
            {
                epCheck.SetError(txtMatKhau, "Mật khẩu không được để trống!");
                isValid = false;
            }

            // 3. Kiểm tra Xác nhận mật khẩu phải khớp với Mật khẩu
            if (string.IsNullOrWhiteSpace(txtXacNhanMatKhau.Text))
            {
                epCheck.SetError(txtXacNhanMatKhau, "Vui lòng nhập lại mật khẩu!");
                isValid = false;
            }
            else if (txtMatKhau.Text != txtXacNhanMatKhau.Text)
            {
                epCheck.SetError(txtXacNhanMatKhau, "Mật khẩu xác nhận không khớp với mật khẩu ban đầu!");
                isValid = false;
            }

            // 4. Kiểm tra Độ tuổi từ Ngày sinh phải >= 18 tuổi
            DateTime ngaySinh = dtpNgaySinh.Value.Date;
            DateTime homNay = DateTime.Now.Date;
            int tuoi = homNay.Year - ngaySinh.Year;
            if (ngaySinh > homNay.AddYears(-tuoi)) tuoi--;

            if (tuoi < 18)
            {
                epCheck.SetError(dtpNgaySinh, "Bạn phải đủ từ 18 tuổi trở lên để đăng ký!");
                isValid = false;
            }

            // 5. Kiểm tra tích chọn Điều khoản dịch vụ
            if (!chkDieuKhoan.Checked)
            {
                epCheck.SetError(chkDieuKhoan, "Bạn phải đồng ý với Điều khoản dịch vụ!");
                isValid = false;
            }

            // Nếu tất cả điều kiện đều hợp lệ
            if (isValid)
            {
                string gioiTinh = rdbNam.Checked ? "Nam" : "Nữ";
                MessageBox.Show(
                    $"Đăng ký tài khoản thành công!\n\n" +
                    $"Tên đăng nhập: {txtTenDangNhap.Text.Trim()}\n" +
                    $"Giới tính: {gioiTinh}\n" +
                    $"Ngày sinh: {dtpNgaySinh.Value:dd/MM/yyyy}",
                    "Thông Báo",
                    MessageBoxButtons.OK,
                    MessageBoxIcon.Information
                );
            }
        }

        // --- XỬ LÝ NÚT LÀM MỚI ---
        private void BtnLamMoi_Click(object sender, EventArgs e)
        {
            txtTenDangNhap.Clear();
            txtMatKhau.Clear();
            txtXacNhanMatKhau.Clear();
            dtpNgaySinh.Value = DateTime.Now;
            rdbNam.Checked = true;
            chkDieuKhoan.Checked = false;
            epCheck.Clear();
            txtTenDangNhap.Focus();
        }
    }
} 
Program.cs
using System;
using System.Windows.Forms;

namespace WindowsFormsApp1
{
    static class Program
    {
        [STAThread]
        static void Main()
        {
            Application.EnableVisualStyles();
            Application.SetCompatibleTextRenderingDefault(false);
            Application.Run(new Form1());
        }
    }
}
BAI 2:
DichVu.cs
namespace WindowsFormsApp1
{
    public class DichVu
    {
        public string TenDichVu { get; set; }
        public decimal DonGia { get; set; }
        public string LoaiDichVu { get; set; }

        public override string ToString()
        {
            return $"{TenDichVu} - {DonGia:N0} VNĐ";
        }
    }
}
Form1.Designer.cs
using System.ComponentModel;
using System.Windows.Forms;

namespace WindowsFormsApp1
{
    partial class Form1
    {
        private IContainer components = null;

        protected override void Dispose(bool disposing)
        {
            if (disposing && (components != null))
            {
                components.Dispose();
            }
            base.Dispose(disposing);
        }

        #region Windows Form Designer generated code
        private void InitializeComponent()
        {
            this.components = new Container();
            this.AutoScaleMode = AutoScaleMode.Font;
            this.ClientSize = new System.Drawing.Size(820, 530);
            this.Text = "Bảng Tính Tiền Dịch Vụ Và Chiết Khấu Đơn Hàng";
        }
        #endregion
    }
}
Form1.cs
using System;
using System.Collections.Generic;
using System.Drawing;
using System.Linq;
using System.Windows.Forms;

namespace WindowsFormsApp1
{
    public partial class Form1 : Form
    {
        private List<DichVu> danhSachDichVuGoc = new List<DichVu>();

        // Controls giao diện
        private ComboBox cboCategory;
        private ListBox lstAvailableServices;
        private ListBox lstSelectedServices;
        private Button btnSelect, btnRemove, btnClearAll;
        private NumericUpDown nudChietKhau;
        private TextBox txtTongTien, txtThanhTien;

        public Form1()
        {
            InitializeComponent();
            InitializeComponentsCustom();
            InitData();
        }

        private void InitializeComponentsCustom()
        {
            this.StartPosition = FormStartPosition.CenterScreen;
            this.FormBorderStyle = FormBorderStyle.FixedSingle;
            this.MaximizeBox = false;

            TableLayoutPanel mainLayout = new TableLayoutPanel
            {
                Dock = DockStyle.Fill,
                RowCount = 3,
                ColumnCount = 1,
                Padding = new Padding(15)
            };
            mainLayout.RowStyles.Add(new RowStyle(SizeType.Absolute, 45F));
            mainLayout.RowStyles.Add(new RowStyle(SizeType.Percent, 100F));
            mainLayout.RowStyles.Add(new RowStyle(SizeType.Absolute, 130F));

            // --- 1. COMBOBOX LOẠI DỊCH VỤ ---
            TableLayoutPanel topLayout = new TableLayoutPanel { Dock = DockStyle.Fill, ColumnCount = 2 };
            topLayout.ColumnStyles.Add(new ColumnStyle(SizeType.Absolute, 110F));
            topLayout.ColumnStyles.Add(new ColumnStyle(SizeType.Percent, 100F));

            cboCategory = new ComboBox { Dock = DockStyle.Fill, DropDownStyle = ComboBoxStyle.DropDownList };
            cboCategory.Items.AddRange(new string[] { "-- Tất cả loại dịch vụ --", "Khám bệnh", "Xét nghiệm", "Chụp X-Quang", "Vắc-xin" });
            cboCategory.SelectedIndex = 0;
            cboCategory.SelectedIndexChanged += CboCategory_SelectedIndexChanged;

            topLayout.Controls.Add(new Label { Text = "Loại dịch vụ:", Anchor = AnchorStyles.Left, AutoSize = true }, 0, 0);
            topLayout.Controls.Add(cboCategory, 1, 0);

            // --- 2. LISTBOX VÀ NÚT CHUYỂN DỊCH VỤ ---
            TableLayoutPanel listLayout = new TableLayoutPanel { Dock = DockStyle.Fill, ColumnCount = 3, RowCount = 1 };
            listLayout.ColumnStyles.Add(new ColumnStyle(SizeType.Percent, 45F));
            listLayout.ColumnStyles.Add(new ColumnStyle(SizeType.Percent, 10F));
            listLayout.ColumnStyles.Add(new ColumnStyle(SizeType.Percent, 45F));

            GroupBox gbAvailable = new GroupBox { Text = "Danh sách dịch vụ", Dock = DockStyle.Fill };
            lstAvailableServices = new ListBox { Dock = DockStyle.Fill, SelectionMode = SelectionMode.One };
            lstAvailableServices.DoubleClick += (s, e) => BtnSelect_Click(s, e);
            gbAvailable.Controls.Add(lstAvailableServices);

            GroupBox gbSelected = new GroupBox { Text = "Dịch vụ đã chọn", Dock = DockStyle.Fill };
            lstSelectedServices = new ListBox { Dock = DockStyle.Fill, SelectionMode = SelectionMode.One };
            lstSelectedServices.DoubleClick += (s, e) => BtnRemove_Click(s, e);
            gbSelected.Controls.Add(lstSelectedServices);

            FlowLayoutPanel pnlButtons = new FlowLayoutPanel
            {
                Dock = DockStyle.Fill,
                FlowDirection = FlowDirection.TopDown,
                WrapContents = false,
                Padding = new Padding(5, 50, 5, 0)
            };

            btnSelect = new Button { Text = ">", Width = 55, Height = 35 };
            btnRemove = new Button { Text = "<", Width = 55, Height = 35 };
            btnClearAll = new Button { Text = "<<", Width = 55, Height = 35 };

            btnSelect.Click += BtnSelect_Click;
            btnRemove.Click += BtnRemove_Click;
            btnClearAll.Click += BtnClearAll_Click;

            pnlButtons.Controls.AddRange(new Control[] { btnSelect, btnRemove, btnClearAll });

            listLayout.Controls.Add(gbAvailable, 0, 0);
            listLayout.Controls.Add(pnlButtons, 1, 0);
            listLayout.Controls.Add(gbSelected, 2, 0);

            // --- 3. NHÓM TÍNH TIỀN ---
            GroupBox gbPayment = new GroupBox { Text = "Thông tin thanh toán", Dock = DockStyle.Fill };
            TableLayoutPanel paymentLayout = new TableLayoutPanel
            {
                Dock = DockStyle.Fill,
                ColumnCount = 4,
                RowCount = 2,
                Padding = new Padding(10)
            };
            paymentLayout.ColumnStyles.Add(new ColumnStyle(SizeType.Percent, 20F));
            paymentLayout.ColumnStyles.Add(new ColumnStyle(SizeType.Percent, 30F));
            paymentLayout.ColumnStyles.Add(new ColumnStyle(SizeType.Percent, 20F));
            paymentLayout.ColumnStyles.Add(new ColumnStyle(SizeType.Percent, 30F));

            txtTongTien = new TextBox { Anchor = AnchorStyles.Left | AnchorStyles.Right, ReadOnly = true, Text = "0 VNĐ" };
            txtThanhTien = new TextBox { Anchor = AnchorStyles.Left | AnchorStyles.Right, ReadOnly = true, Text = "0 VNĐ", Font = new Font(this.Font, FontStyle.Bold) };

            nudChietKhau = new NumericUpDown
            {
                Anchor = AnchorStyles.Left | AnchorStyles.Right,
                Minimum = 0,
                Maximum = 100,
                Value = 0,
                DecimalPlaces = 0
            };
            nudChietKhau.ValueChanged += (s, e) => TinhTongTien();

            paymentLayout.Controls.Add(new Label { Text = "Tổng tiền chưa giảm:", Anchor = AnchorStyles.Left, AutoSize = true }, 0, 0);
            paymentLayout.Controls.Add(txtTongTien, 1, 0);
            paymentLayout.Controls.Add(new Label { Text = "Tỷ lệ chiết khấu (%):", Anchor = AnchorStyles.Left, AutoSize = true }, 2, 0);
            paymentLayout.Controls.Add(nudChietKhau, 3, 0);

            paymentLayout.Controls.Add(new Label { Text = "Thành tiền thanh toán:", Anchor = AnchorStyles.Left, AutoSize = true }, 0, 1);
            paymentLayout.Controls.Add(txtThanhTien, 1, 1);

            gbPayment.Controls.Add(paymentLayout);

            mainLayout.Controls.Add(topLayout, 0, 0);
            mainLayout.Controls.Add(listLayout, 0, 1);
            mainLayout.Controls.Add(gbPayment, 0, 2);

            this.Controls.Add(mainLayout);
        }

        private void InitData()
        {
            danhSachDichVuGoc.Add(new DichVu { TenDichVu = "Khám tổng quát", DonGia = 150000, LoaiDichVu = "Khám bệnh" });
            danhSachDichVuGoc.Add(new DichVu { TenDichVu = "Khám chuyên khoa", DonGia = 250000, LoaiDichVu = "Khám bệnh" });
            danhSachDichVuGoc.Add(new DichVu { TenDichVu = "Xét nghiệm máu tổng phân tích", DonGia = 200000, LoaiDichVu = "Xét nghiệm" });
            danhSachDichVuGoc.Add(new DichVu { TenDichVu = "Xét nghiệm đường huyết", DonGia = 100000, LoaiDichVu = "Xét nghiệm" });
            danhSachDichVuGoc.Add(new DichVu { TenDichVu = "Chụp X-Quang Phổi", DonGia = 180000, LoaiDichVu = "Chụp X-Quang" });
            danhSachDichVuGoc.Add(new DichVu { TenDichVu = "Chụp X-Quang Cột sống", DonGia = 220000, LoaiDichVu = "Chụp X-Quang" });
            danhSachDichVuGoc.Add(new DichVu { TenDichVu = "Vắc-xin Cúm mùa", DonGia = 350000, LoaiDichVu = "Vắc-xin" });
            danhSachDichVuGoc.Add(new DichVu { TenDichVu = "Vắc-xin Viêm gan B", DonGia = 300000, LoaiDichVu = "Vắc-xin" });

            LoadAvailableServices();
        }

        private void LoadAvailableServices()
        {
            lstAvailableServices.Items.Clear();
            string selectedCategory = cboCategory.SelectedItem?.ToString();

            var filtered = danhSachDichVuGoc.Where(x =>
                selectedCategory == null ||
                selectedCategory == "-- Tất cả loại dịch vụ --" ||
                x.LoaiDichVu == selectedCategory
            );

            foreach (var item in filtered)
            {
                lstAvailableServices.Items.Add(item);
            }
        }

        private void CboCategory_SelectedIndexChanged(object sender, EventArgs e)
        {
            LoadAvailableServices();
        }

        private void BtnSelect_Click(object sender, EventArgs e)
        {
            if (lstAvailableServices.SelectedItem != null)
            {
                DichVu selected = lstAvailableServices.SelectedItem as DichVu;
                if (selected != null)
                {
                    lstSelectedServices.Items.Add(selected);
                    TinhTongTien();
                }
            }
        }

        private void BtnRemove_Click(object sender, EventArgs e)
        {
            if (lstSelectedServices.SelectedItem != null)
            {
                lstSelectedServices.Items.Remove(lstSelectedServices.SelectedItem);
                TinhTongTien();
            }
        }

        private void BtnClearAll_Click(object sender, EventArgs e)
        {
            if (lstSelectedServices.Items.Count > 0)
            {
                lstSelectedServices.Items.Clear();
                TinhTongTien();
            }
        }

        private void TinhTongTien()
        {
            decimal tongTien = 0;
            foreach (DichVu item in lstSelectedServices.Items)
            {
                tongTien += item.DonGia;
            }

            decimal tyLeChietKhau = nudChietKhau.Value;
            decimal tienChietKhau = tongTien * (tyLeChietKhau / 100m);
            decimal thanhTien = tongTien - tienChietKhau;

            txtTongTien.Text = $"{tongTien:N0} VNĐ";
            txtThanhTien.Text = $"{thanhTien:N0} VNĐ";
        }
    }
}
Program.cs
using System;
using System.Windows.Forms;

namespace WindowsFormsApp1
{
    static class Program
    {
        [STAThread]
        static void Main()
        {
            Application.EnableVisualStyles();
            Application.SetCompatibleTextRenderingDefault(false);
            Application.Run(new Form1());
        }
    }
}

