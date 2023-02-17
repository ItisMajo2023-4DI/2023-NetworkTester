# Traccia

Realizzare un network monitor in grado di:

1. Mostrare in un elenco una serie di test verso alcuni Host raggiungibili in rete
2. L'elenco dei test va letto da un file
3. Il risultato dei test va salvato in un file
4. I test possibili sono di tre tipi: ping, telnet e HTTP Get
5. Il lancio della batteria di test va legato ad un bottone

![Esempio Network Test](EsempioNetworkTest.png)

## La struttura del file dei test

Source;Name;Type;IP;Port;URL;Enable
Localhost;PC;Ping;127.0.0.1;0;;true
Localhost;PC;Telnet;127.0.0.1;80;;true
Google;google;Ping;google.com;0;;false
Wikipedia;wiki;Ping;wikipedia.org;0;;true
IEC104Master;Embedded121 IP 1;Ping;10.100.0.194;0;;true
IEC104Master;Embedded121 IP 1;Telnet;10.100.0.194;2404;;true
IEC104Master;Embedded120 IP 1;Ping;10.100.0.120;0;;false
IEC104Master;Embedded120 IP 1;Telnet;10.100.0.120;2404;;false
n3uron;TestN3erun;Ping;10.21.0.223;0;;true
n3uron;TestN3erun;Telnet;10.21.0.223;8081;;true
NordexSoap;TestNordexSoap_Bruyere;Ping;217.128.242.98;0;;true
NordexSoap;TestNordexSoap_LesCarreau;Ping;217.128.20.202;0;;true
SenvionMail;SenvionMail;Ping;outlook.office365.com;0;;true
SenvionMail;SenvionMail;Telnet;outlook.office365.com;993;;true
EnerconOpcXml;EnerconTestVolturara;Ping;10.80.0.22;0;;true
EnerconOpcXml;EnerconTestVolturara;Telnet;10.80.0.22;5005;;true
SQLServer;Consuntive;Ping;10.100.0.105;0;;true
SQLServer;Consuntive;Telnet;10.100.0.105;1433;;true
SSH;Brunetti;Ping;127.0.0.1;0;;true
SSH;Brunetti;Telnet;127.0.0.1;22;;true
SSH;BrunettiSS;Ping;127.0.0.1;0;;true
SSH;BrunettiSS;Telnet;127.0.0.1;22;;true
SSH;LinuxSSH;Ping;10.100.0.122;0;;true
SSH;LinuxSSH;Telnet;10.100.0.122;22;;true
FTP;Orsara;Ping;10.100.0.105;0;;true
FTP;Orsara;Telnet;10.100.0.105;21;;true
WSSH;WindowsSSH;Ping;10.100.0.192;0;;true
WSSH;WindowsSSH;Telnet;10.100.0.192;22;;true
Diagnostica;Inverter 01;http;https://it.wikipedia.org/wiki/Turbina_eolica;80;;true


## Progetto di partenza
Realizzare in c# una applicazione in grado di eseguire il ping su un indirizzo indicato in una textbox. 

(using System.Net.NetworkInformation;)

- durante l'operazione il cursore del mouse deve risultare in attesa e i campi status e time devono essere vuoti
- ad operazione terminata visualizzare il tempo e lo status
- per eseguire i ping di prova individuare l'indirizzo IP dei computer del laboratorio, del proprio smartphone e di altri nodi sulla rete
- aggiungere icone di successo/errore/linea lenta

Codice di esempio:

            this.Cursor = Cursors.Wait
            txtStatus.Text = "";
            txtMs.Text = "";
            string Indirizzo = txtIP.Text;
           
            Ping pinger = new Ping();
            PingReply reply = pinger.Send(Indirizzo);
            string status = reply.Status.ToString();
            string millisec = reply.RoundtripTime.ToString();
            txtStatus.Text = status;
            txtMs.Text = millisec;
            this.Cursor = Cursors.Arrow;
