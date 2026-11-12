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
bai 3:
Product.cs
namespace WindowsFormsApp1
{
    public class Product
    {
        public string ProductId { get; set; }
        public string ProductName { get; set; }
        public decimal UnitPrice { get; set; }
        public int Quantity { get; set; }
        public string Category { get; set; }
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
            this.ClientSize = new System.Drawing.Size(950, 650);
            this.Text = "Quản Lý Danh Sách Sản Phẩm";
        }
        #endregion
    }
}
Form1.cs
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Drawing;
using System.Linq;
using System.Windows.Forms;

namespace WindowsFormsApp1
{
    public partial class Form1 : Form
    {
        private BindingList<Product> gocDanhSach = new BindingList<Product>();
        private BindingSource bindingSource = new BindingSource();

        // Controls Nhập liệu
        private TextBox txtProductId, txtProductName;
        private NumericUpDown nudUnitPrice, nudQuantity;
        private ComboBox cboCategory;

        // Controls Chức năng & Tìm kiếm
        private TextBox txtSearch;
        private Button btnAdd, btnEdit, btnDelete, btnClear;

        // DataGridView & ErrorProvider
        private DataGridView dgvProducts;
        private ErrorProvider errorProvider;

        public Form1()
        {
            InitializeComponent();
            InitializeComponentsCustom();
            InitData();
        }

        private void InitializeComponentsCustom()
        {
            this.StartPosition = FormStartPosition.CenterScreen;
            errorProvider = new ErrorProvider { BlinkStyle = ErrorBlinkStyle.NeverBlink };

            TableLayoutPanel mainLayout = new TableLayoutPanel
            {
                Dock = DockStyle.Fill,
                RowCount = 3,
                ColumnCount = 1,
                Padding = new Padding(12)
            };
            mainLayout.RowStyles.Add(new RowStyle(SizeType.Absolute, 200F)); // Khu nhập liệu + Chức năng
            mainLayout.RowStyles.Add(new RowStyle(SizeType.Absolute, 50F));  // Tìm kiếm
            mainLayout.RowStyles.Add(new RowStyle(SizeType.Percent, 100F));  // DataGridView

            // --- 1. GROUPBOX THÔNG TIN SẢN PHẨM & CHỨC NĂNG ---
            GroupBox gbProductInfo = new GroupBox { Text = "Thông tin sản phẩm", Dock = DockStyle.Fill };
            TableLayoutPanel inputContentLayout = new TableLayoutPanel
            {
                Dock = DockStyle.Fill,
                ColumnCount = 2,
                RowCount = 1
            };
            inputContentLayout.ColumnStyles.Add(new ColumnStyle(SizeType.Percent, 70F));
            inputContentLayout.ColumnStyles.Add(new ColumnStyle(SizeType.Percent, 30F));

            // Controls nhập thông tin
            TableLayoutPanel infoLayout = new TableLayoutPanel
            {
                Dock = DockStyle.Fill,
                ColumnCount = 4,
                RowCount = 3,
                Padding = new Padding(5)
            };
            for (int i = 0; i < 4; i++)
            {
                infoLayout.ColumnStyles.Add(new ColumnStyle(SizeType.Percent, i % 2 == 0 ? 15F : 35F));
            }

            txtProductId = new TextBox { Anchor = AnchorStyles.Left | AnchorStyles.Right };
            txtProductName = new TextBox { Anchor = AnchorStyles.Left | AnchorStyles.Right };

            nudUnitPrice = new NumericUpDown
            {
                Anchor = AnchorStyles.Left | AnchorStyles.Right,
                Minimum = 0,
                Maximum = 1000000000,
                Increment = 10000,
                ThousandsSeparator = true
            };

            nudQuantity = new NumericUpDown
            {
                Anchor = AnchorStyles.Left | AnchorStyles.Right,
                Minimum = 0,
                Maximum = 10000,
                Value = 1
            };

            cboCategory = new ComboBox { Anchor = AnchorStyles.Left | AnchorStyles.Right, DropDownStyle = ComboBoxStyle.DropDownList };
            cboCategory.Items.AddRange(new string[] { "Điện tử", "Gia dụng", "Thời trang", "Thực phẩm", "Văn phòng phẩm" });
            if (cboCategory.Items.Count > 0) cboCategory.SelectedIndex = 0;

            infoLayout.Controls.Add(new Label { Text = "Mã SP:", Anchor = AnchorStyles.Left, AutoSize = true }, 0, 0);
            infoLayout.Controls.Add(txtProductId, 1, 0);
            infoLayout.Controls.Add(new Label { Text = "Tên SP:", Anchor = AnchorStyles.Left, AutoSize = true }, 2, 0);
            infoLayout.Controls.Add(txtProductName, 3, 0);

            infoLayout.Controls.Add(new Label { Text = "Đơn giá:", Anchor = AnchorStyles.Left, AutoSize = true }, 0, 1);
            infoLayout.Controls.Add(nudUnitPrice, 1, 1);
            infoLayout.Controls.Add(new Label { Text = "Số lượng:", Anchor = AnchorStyles.Left, AutoSize = true }, 2, 1);
            infoLayout.Controls.Add(nudQuantity, 3, 1);

            infoLayout.Controls.Add(new Label { Text = "Danh mục:", Anchor = AnchorStyles.Left, AutoSize = true }, 0, 2);
            infoLayout.Controls.Add(cboCategory, 1, 2);

            // GroupBox Chức năng
            GroupBox gbActions = new GroupBox { Text = "Chức năng", Dock = DockStyle.Fill };
            FlowLayoutPanel pnlButtons = new FlowLayoutPanel
            {
                Dock = DockStyle.Fill,
                FlowDirection = FlowDirection.TopDown,
                Padding = new Padding(10, 10, 0, 0)
            };

            btnAdd = new Button { Text = "Thêm", Width = 90, Height = 30 };
            btnEdit = new Button { Text = "Sửa", Width = 90, Height = 30 };
            btnDelete = new Button { Text = "Xóa", Width = 90, Height = 30 };
            btnClear = new Button { Text = "Làm mới", Width = 90, Height = 30 };

            btnAdd.Click += BtnAdd_Click;
            btnEdit.Click += BtnEdit_Click;
            btnDelete.Click += BtnDelete_Click;
            btnClear.Click += (s, e) => ClearInputFields();

            pnlButtons.Controls.AddRange(new Control[] { btnAdd, btnEdit, btnDelete, btnClear });
            gbActions.Controls.Add(pnlButtons);

            inputContentLayout.Controls.Add(infoLayout, 0, 0);
            inputContentLayout.Controls.Add(gbActions, 1, 0);
            gbProductInfo.Controls.Add(inputContentLayout);

            // --- 2. KHU VỰC TÌM KIẾM ---
            GroupBox gbSearch = new GroupBox { Text = "Tìm kiếm sản phẩm", Dock = DockStyle.Fill };
            FlowLayoutPanel pnlSearch = new FlowLayoutPanel { Dock = DockStyle.Fill, AutoScroll = true };

            txtSearch = new TextBox { Width = 250 };
            txtSearch.TextChanged += TxtSearch_TextChanged;

            pnlSearch.Controls.Add(new Label { Text = "Nhập tên SP để tìm kiếm:", AutoSize = true, Margin = new Padding(0, 5, 0, 0) });
            pnlSearch.Controls.Add(txtSearch);
            gbSearch.Controls.Add(pnlSearch);

            // --- 3. DATAGRIDVIEW HIỂN THỊ SẢN PHẨM ---
            dgvProducts = new DataGridView
            {
                Dock = DockStyle.Fill,
                AutoGenerateColumns = false,
                SelectionMode = DataGridViewSelectionMode.FullRowSelect,
                MultiSelect = false,
                ReadOnly = true,
                AllowUserToAddRows = false,
                AutoSizeColumnsMode = DataGridViewAutoSizeColumnsMode.Fill
            };

            dgvProducts.Columns.Add(new DataGridViewTextBoxColumn { DataPropertyName = "ProductId", HeaderText = "Mã Sản Phẩm", FillWeight = 90 });
            dgvProducts.Columns.Add(new DataGridViewTextBoxColumn { DataPropertyName = "ProductName", HeaderText = "Tên Sản Phẩm", FillWeight = 160 });
            dgvProducts.Columns.Add(new DataGridViewTextBoxColumn { DataPropertyName = "UnitPrice", HeaderText = "Đơn Giá (VNĐ)", FillWeight = 110, DefaultCellStyle = new DataGridViewCellStyle { Format = "N0", Alignment = DataGridViewContentAlignment.MiddleRight } });
            dgvProducts.Columns.Add(new DataGridViewTextBoxColumn { DataPropertyName = "Quantity", HeaderText = "Số Lượng", FillWeight = 70, DefaultCellStyle = new DataGridViewCellStyle { Alignment = DataGridViewContentAlignment.MiddleCenter } });
            dgvProducts.Columns.Add(new DataGridViewTextBoxColumn { DataPropertyName = "Category", HeaderText = "Danh Mục", FillWeight = 110 });

            dgvProducts.SelectionChanged += DgvProducts_SelectionChanged;

            mainLayout.Controls.Add(gbProductInfo, 0, 0);
            mainLayout.Controls.Add(gbSearch, 0, 1);
            mainLayout.Controls.Add(dgvProducts, 0, 2);

            this.Controls.Add(mainLayout);
        }

        private void InitData()
        {
            gocDanhSach.Add(new Product { ProductId = "SP01", ProductName = "Laptop Dell XPS 13", UnitPrice = 28500000, Quantity = 5, Category = "Điện tử" });
            gocDanhSach.Add(new Product { ProductId = "SP02", ProductName = "Nồi cơm điện Sunhouse", UnitPrice = 850000, Quantity = 12, Category = "Gia dụng" });
            gocDanhSach.Add(new Product { ProductId = "SP03", ProductName = "Áo sơ mi Nam", UnitPrice = 350000, Quantity = 30, Category = "Thời trang" });

            bindingSource.DataSource = gocDanhSach;
            dgvProducts.DataSource = bindingSource;
        }

        // --- VALIDATION DỮ LIỆU ---
        private bool ValidateInput(bool isAdding)
        {
            errorProvider.Clear();
            bool isValid = true;

            if (string.IsNullOrWhiteSpace(txtProductId.Text))
            {
                errorProvider.SetError(txtProductId, "Mã sản phẩm không được để trống!");
                isValid = false;
            }
            else if (isAdding && gocDanhSach.Any(p => p.ProductId.Equals(txtProductId.Text.Trim(), StringComparison.OrdinalIgnoreCase)))
            {
                errorProvider.SetError(txtProductId, "Mã sản phẩm đã tồn tại!");
                isValid = false;
            }

            if (string.IsNullOrWhiteSpace(txtProductName.Text))
            {
                errorProvider.SetError(txtProductName, "Tên sản phẩm không được để trống!");
                isValid = false;
            }

            return isValid;
        }

        // --- NÚT THÊM ---
        private void BtnAdd_Click(object sender, EventArgs e)
        {
            if (!ValidateInput(isAdding: true)) return;

            Product p = new Product
            {
                ProductId = txtProductId.Text.Trim(),
                ProductName = txtProductName.Text.Trim(),
                UnitPrice = nudUnitPrice.Value,
                Quantity = (int)nudQuantity.Value,
                Category = cboCategory.SelectedItem?.ToString()
            };

            gocDanhSach.Add(p);
            ApplyFilter();
            MessageBox.Show("Thêm sản phẩm thành công!", "Thông báo", MessageBoxButtons.OK, MessageBoxIcon.Information);
            ClearInputFields();
        }

        // --- NÚT SỬA ---
        private void BtnEdit_Click(object sender, EventArgs e)
        {
            if (dgvProducts.CurrentRow == null) return;
            if (!ValidateInput(isAdding: false)) return;

            Product selected = dgvProducts.CurrentRow.DataBoundItem as Product;
            if (selected != null)
            {
                selected.ProductName = txtProductName.Text.Trim();
                selected.UnitPrice = nudUnitPrice.Value;
                selected.Quantity = (int)nudQuantity.Value;
                selected.Category = cboCategory.SelectedItem?.ToString();

                bindingSource.ResetBindings(false);
                MessageBox.Show("Cập nhật thông tin sản phẩm thành công!", "Thông báo", MessageBoxButtons.OK, MessageBoxIcon.Information);
            }
        }

        // --- NÚT XÓA ---
        private void BtnDelete_Click(object sender, EventArgs e)
        {
            if (dgvProducts.CurrentRow == null) return;

            Product selected = dgvProducts.CurrentRow.DataBoundItem as Product;
            if (selected != null)
            {
                DialogResult dr = MessageBox.Show($"Bạn có chắc chắn muốn xóa sản phẩm [{selected.ProductId}] - {selected.ProductName}?", "Xác nhận xóa", MessageBoxButtons.YesNo, MessageBoxIcon.Question);
                if (dr == DialogResult.Yes)
                {
                    gocDanhSach.Remove(selected);
                    ApplyFilter();
                    ClearInputFields();
                    MessageBox.Show("Xóa sản phẩm thành công!", "Thông báo", MessageBoxButtons.OK, MessageBoxIcon.Information);
                }
            }
        }

        // --- ĐẨY DỮ LIỆU TỪ DATAGRIDVIEW LÊN CÁC Ô NHẬP LIỆU ---
        private void DgvProducts_SelectionChanged(object sender, EventArgs e)
        {
            if (dgvProducts.CurrentRow != null)
            {
                Product selected = dgvProducts.CurrentRow.DataBoundItem as Product;
                if (selected != null)
                {
                    txtProductId.Text = selected.ProductId;
                    txtProductId.ReadOnly = true; // Khóa Mã SP khi chọn dòng để sửa
                    txtProductName.Text = selected.ProductName;
                    nudUnitPrice.Value = selected.UnitPrice >= 0 ? selected.UnitPrice : 0;
                    nudQuantity.Value = selected.Quantity >= 0 ? selected.Quantity : 1;
                    cboCategory.SelectedItem = selected.Category;
                }
            }
        }

        // --- TÌM KIẾM TỨC THỜI THEO TÊN SP ---
        private void TxtSearch_TextChanged(object sender, EventArgs e)
        {
            ApplyFilter();
        }

        private void ApplyFilter()
        {
            string keyword = txtSearch.Text.Trim().ToLower();
            var filtered = gocDanhSach.Where(p => string.IsNullOrEmpty(keyword) || p.ProductName.ToLower().Contains(keyword)).ToList();
            bindingSource.DataSource = new BindingList<Product>(filtered);
        }

        private void ClearInputFields()
        {
            txtProductId.ReadOnly = false;
            txtProductId.Clear();
            txtProductName.Clear();
            nudUnitPrice.Value = 0;
            nudQuantity.Value = 1;
            if (cboCategory.Items.Count > 0) cboCategory.SelectedIndex = 0;
            errorProvider.Clear();
            txtProductId.Focus();
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
