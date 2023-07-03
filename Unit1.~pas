unit Unit1;

interface

uses
  Windows, Messages, SysUtils, Variants, Classes, Graphics, Controls, Forms,
  Dialogs, StdCtrls, jpeg, ExtCtrls, DB, ADODB, Grids, DBGrids, ComCtrls,
  DBTables, DBClient, MConnect;

type
  TForm1 = class(TForm)
    Image1: TImage;
    Label1: TLabel;
    Label2: TLabel;
    Label3: TLabel;
    Label4: TLabel;
    Label5: TLabel;
    Label6: TLabel;
    Editkode: TEdit;
    Editnama: TEdit;
    Editharga: TEdit;
    Editstok: TEdit;
    ADD: TButton;
    DELETE: TButton;
    EDIT: TButton;
    LIHATDATA: TButton;
    DateTimePickerumur: TDateTimePicker;
    DataSource1: TDataSource;
    ADOConnection1: TADOConnection;
    ADOQuery1: TADOQuery;
    DBGrid1: TDBGrid;
    procedure ADDClick(Sender: TObject);
    procedure LIHATDATAClick(Sender: TObject);
    procedure FormCreate(Sender: TObject);
    procedure EDITClick(Sender: TObject);
    procedure DELETEClick(Sender: TObject);
  private
    { Private declarations }
  public
    { Public declarations }
  end;

var
  Form1: TForm1;

implementation

uses Unit2, Unit3;

{$R *.dfm}

procedure TForm1.ADDClick(Sender: TObject);
begin
begin
// Validasi field Kode_obat tidak boleh kosong
  if Length(Editkode.Text) < 1 then
  begin
  MessageDlg('Field Kode_obat tidak boleh kosong!',mtWarning,[mbOK],0);
  Exit;
  end;
// validasi duplikat Kode_obat
with ADOQuery1 do
begin
   Active:=False;
   SQL.Clear;
   SQL.Text :=
   ' SELECT * FROM GUDANG WHERE kode_obat = ' + Editkode.Text + ';  ';

   Active := True;
   end;
   //Tampilkan pesan jika terjdai duplikasi
   //dan keluar proses add
   if ADOQuery1.RecordCount > 0 then
   begin
   MessageDlg('Terjadi Duplikasi Kode_obat. Silahkan ganti dengan yang baru!',mtError,[mbOK],0);
   Editkode.Clear;
   Editkode.SetFocus;
   //keluar dari proses insert
   Exit;
   end;
   end;

//proses simpan data obat
with ADOQuery1 do
begin
SQL.Clear;
SQL.Text :=' INSERT INTO GUDANG(kode_obat,nama_obat,harga_obat,tanggal_kadaluarsa,jumlah_stok) VALUES (' + Editkode.Text + ' , ' +
QuotedStr(Editnama.Text) + ' , ' + Editharga.Text + ' , ' +'#' + DateToStr(DateTimePickerumur.Date) +
'#' + ' , ' + Editstok.Text + ');';
//MessageDlg(SQL.Text,mtInformation,[mbOK],0);
//Exit;
ExecSQL;
MessageDlg('Data sudah tersimpan',mtInformation,[mbOK],0);
// panggil event formcreate untuk merefresh data pada dbgrid
FormCreate(Sender);
end;
end;

procedure TForm1.LIHATDATAClick(Sender: TObject);
begin
Form3.QuickRep1.Preview
end;

procedure TForm1.FormCreate(Sender: TObject);
begin
with ADOQuery1 do
begin
  Active :=False;
  SQL.Clear;
  SQL.Text :=' SELECT * FROM GUDANG ';
  Active := True  ;
end;
end;

procedure TForm1.EDITClick(Sender: TObject);
begin
// validasi field Kode tidak boleh kosong
if Length(Editkode.Text) < 1 then
begin
MessageDlg('Pilih salah satu data pada DBGRID!',mtWarning,[mbOK],0);
Exit;
end;
// proses update obat
with ADOQuery1 do
begin
SQL.Clear;
SQL.Text :=
' UPDATE TABLE SET ' +
' nama_obat = ' + QuotedStr(Editnama.Text) + ' , ' +
' harga_obat = ' + Editharga.Text + ' , ' +
' tanggal_kadaluarsa = ' + '#' + DateToStr(DateTimePickerumur.Date) + '#' +
' , ' +
' jumlah_stok = ' + Editstok.Text +
' WHERE kode_obat = ' + Editkode.Text;
ExecSQL;
MessageDlg('Data sudah diperbaharui',mtInformation,[mbOK],0);
end;
// panggil event formcreate untuk merefresh data pada dbgrid
FormCreate(Sender);
end;

procedure TForm1.DELETEClick(Sender: TObject);
begin
// validasi field kode tidak boleh kosong
if Length(Editkode.Text) < 1 then
begin
MessageDlg('Pilih salah satu data pada DBGRID!',mtWarning,[mbOK],0);
Exit;
end;
// proses hapus Data
if Application.MessageBox('Apakah anda akan menghapus data ini?','Warning',MB_YESNO) = mrYes then
begin
with ADOQuery1 do
begin
SQL.Clear;
SQL.Text :=' DELETE FROM TABLE WHERE kode_obat = ' + Editkode.Text;
ExecSQL;
MessageDlg('Data sudah terhapus',mtInformation,[mbOK],0);
end;
end;
// panggil event formcreate untuk merefresh data pada dbgrid
FormCreate(Sender);
end;


end.



