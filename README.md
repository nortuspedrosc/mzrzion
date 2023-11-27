# Prodecures de controle de Timer e Arquivo .ini
### *Colocar o arquivo Config.ini na mesma pasta do Macx.exe*

### Inserir a var no Alxor32 = XTimeoutMestre: Integer;

## UMenu
### No Uses do UMenu chamar o IniFiles

### Inserir Timer no UMenu e setar seu interval para = 600.000 milesegundos = 10 minutos

## Procedures a serem criadas no UMenu
### procedure TFMenu.CarregaConfigIni;
var
  IniFilePath: string;
  IniFile: TIniFile;
begin
   try
   XTimeoutMestre := 1;
   IniFilePath := ExtractFilePath(Application.ExeName) + 'config.ini';
           if SysUtils.FileExists(IniFilePath) then
               begin
                try
                   IniFile := TIniFile.Create(IniFilePath);
                   XTimeoutMestre := IniFile.ReadInteger('PARAMETROS', 'Ativar', 1);
               finally
                   IniFile.Free;
               end;
           end;
  except
    on E: Exception do
      ShowMessage('Erro: ' + E.Message);
    end;
end;

### procedure TFMenu.tControleMestreTimer(Sender: TObject);
begin
   if (FMenu.EdUsuario.Text = 'SYSTEM LORD') and (XTimeoutMestre = 1) then
       Begin
           tControleMestre.Enabled := false;
           AbrirForm(TFLogoff1, FLogoff1, 1);
           tControleMestre.Enabled := true;
       end;
end;
