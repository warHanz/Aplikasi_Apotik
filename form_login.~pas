unit form_login;

interface

uses
  Windows, Messages, SysUtils, Variants, Classes, Graphics, Controls, Forms,
  Dialogs, StdCtrls, DB, ADODB, jpeg, ExtCtrls, XPMan;

type
  Tlogin = class(TForm)
    Image1: TImage;
    Image2: TImage;
    chk1: TCheckBox;
    lbl1: TLabel;
    con1: TADOConnection;
    qry1: TADOQuery;
    edtuser: TEdit;
    edtpass: TEdit;
    XPManifest1: TXPManifest;
    Image3: TImage;
    procedure chk1Click(Sender: TObject);
    procedure FormShow(Sender: TObject);
    procedure Image2Click(Sender: TObject);
    procedure Image3Click(Sender: TObject);
  private
    { Private declarations }
  public
    { Public declarations }
  end;

var
  login: Tlogin;
  LAGI  : Integer;

implementation

uses unit1;

{$R *.dfm}

function SetCueBanner(const Edit: TEdit;
const Placeholder: String): Boolean;
const
EM_SETCUEBANNER = $1501; 
var
UniStr: WideString;
begin
UniStr := Placeholder;
SendMessage(Edit.Handle, EM_SETCUEBANNER, WParam(True),LParam(UniStr));
Result := GetLastError() = ERROR_SUCCESS;
end;

procedure Tlogin.chk1Click(Sender: TObject);
begin
if  chk1.Checked then
   begin
      Edtpass.PasswordChar:=#0
   end
   else
      edtpass.PasswordChar:=#149;
end;

procedure Tlogin.FormShow(Sender: TObject);
begin
SetCueBanner(edtuser, 'Username');
SetCueBanner(edtpass, 'Password');
end;

procedure Tlogin.Image2Click(Sender: TObject);
begin
if (edtuser.text='') and (edtpass.text='') then
  begin
    MessageDlg('Username dan Password masih kosong!',mtWarning,[mbOK],0);
    Exit;
    edtuser.SetFocus
  end
  else
if (edtuser.text='') then
  begin
    MessageDlg('Username masih kosong!',mtWarning,[mbOK],0);
    Exit;
    edtuser.SetFocus
  end
  else
if (edtpass.text='') then
  begin
    MessageDlg('Password masih kosong!',mtWarning,[mbOK],0);
    Exit;
    edtpass.SetFocus
  end
  else
If (qry1.LOCATE('user',Edtuser.Text,[])) and (qry1.LOCATE('pass',edtpass.Text,[]))
    and (LAGI<=2)
then
  begin
    Form1.Show;
  end
  else
  begin
    MessageDlg('Pastikan username dan password sudah benar!',mtWarning,[MBOK],0);
    edtuser.SetFocus;
    LAGI:=LAGI+1;

    if LAGI>2 then
      begin
        MessageDlg('Sudah melakukan percobaan login 3x, HUBUNGI ADMINISTRATOR!',mtWarning,[MBOK],0);
        Application.Terminate;
      end;
    end;
end;

procedure Tlogin.Image3Click(Sender: TObject);
begin
Application.Terminate;
end;

end.
