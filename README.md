# -
c#메모장
using System;
using System.Drawing;
using System.IO;
using System.Runtime.Serialization.Formatters;
using System.Text;
using System.Windows.Forms;


namespace WindowsFormsProject
{
    public partial class Test_memo : Form
    {
        private System.Windows.Forms.Timer timer1 = new System.Windows.Forms.Timer();

        
        private Font _originalFont;
        public Test_memo()
        {
            InitializeComponent();

        _originalFont = memo.Font;

        }

        ToolTip toolTip = new ToolTip();
        private string _currentFilePath = null;


        private void mmm_Load(object sender, EventArgs e)
        {
            Message.Text = "안녕하세요";
            timer1.Interval = 1000;
            timer1.Tick += timer1_Tick;
            timer1.Start();
            newtabba.ToolTipText = "새 탭";
            openicon.ToolTipText = "열기";
            saveicon.ToolTipText = "다른 이름으로 저장";
            anothersaveicon.ToolTipText = "복사";
            cuticon.ToolTipText = "자르기";
            patcion.ToolTipText = "붙여넣기";
            fonticon.ToolTipText = "글꼴";
            coloricon.ToolTipText = "색상";
            inicon.ToolTipText = "확대";
            outicon.ToolTipText = "축소";
            zoomicon.ToolTipText = "원래대로";
            SSAVEICON.ToolTipText = "저장";
            dlsthoicon.ToolTipText = "인쇄";
            ALFLQHRLCION.ToolTipText = "미리보기";
            FINDICON.ToolTipText = "찾기";
            JICON.ToolTipText = "줄 이동";
            PAICON.ToolTipText = "페이지 설정";
            NNEWICON.ToolTipText = "새 창";
        }

        private void timer1_Tick(object sender, EventArgs e)
        {
            Time.Text = DateTime.Now.ToLongTimeString();
        }

        private void openOToolStripMenuItem_Click(object sender, EventArgs e)
        {
            openFileDialog1.Filter = "텍스트 문서(*.txt)|*.txt|모든 파일|*.*";
            openFileDialog1.FilterIndex = 1;
            openFileDialog1.InitialDirectory = @"D:\SUUP";
            openFileDialog1.Title = "텍스트 파일 열기";

            if (openFileDialog1.ShowDialog() == DialogResult.OK)
            {
                string File_Name = openFileDialog1.FileName;
                StreamReader str = new StreamReader(File_Name, Encoding.UTF8);
                memo.Text = str.ReadToEnd();
                str.Close();
            }
        }

        private void saveSToolStripMenuItem_Click(object sender, EventArgs e)
        {
            saveFileDialog1.Filter = "텍스트 문서(*.txt)|*.txt|모든 파일|*.*";
            saveFileDialog1.OverwritePrompt = true;

            if (saveFileDialog1.ShowDialog() == DialogResult.OK)
            {
                string File_Name = saveFileDialog1.FileName;
                StreamWriter str = new StreamWriter(File_Name, false, Encoding.UTF8);
                str.Write(memo.Text);
                str.Flush();
                str.Close();

                _currentFilePath = File_Name;
            }
        }

        private void exitEToolStripMenuItem_Click(object sender, EventArgs e)
        {
            this.Close();
        }

        private void fileFToolStripMenuItem_Click(object sender, EventArgs e)
        {

        }

        private void 폰트ToolStripMenuItem_Click(object sender, EventArgs e)
        {
            if (fontDialog1.ShowDialog() == DialogResult.OK)
            {
                memo.Font = fontDialog1.Font;
                _originalFont = fontDialog1.Font;
            }

            Message.Text = "";
        }

        private void 색상ToolStripMenuItem_Click(object sender, EventArgs e)
        {
          
            if (colorDialog1.ShowDialog() == DialogResult.OK)
            {
                memo.ForeColor = colorDialog1.Color;
            }
            Message.Text = "";
        }

        private void 확대ToolStripMenuItem1_Click(object sender, EventArgs e)
        {
         
            var currentFont = memo.Font;
            memo.Font = new Font(currentFont.FontFamily, currentFont.Size + 2, currentFont.Style);
            Message.Text = "";
        }

        private void 축소ToolStripMenuItem1_Click(object sender, EventArgs e)
        {
           
            var currentFont = memo.Font;
            memo.Font = new Font(currentFont.FontFamily, currentFont.Size - 2, currentFont.Style);
            Message.Text = "";
        }

        private void 원래대로돌아가기ToolStripMenuItem_Click(object sender, EventArgs e)
        {
            
            memo.Font = _originalFont;
            Message.Text = "";
        }

        private void 복사하기ToolStripMenuItem_Click(object sender, EventArgs e)
        {
          

            if (!string.IsNullOrEmpty(memo.SelectedText))
            {
               
                Clipboard.SetText(memo.SelectedText);
            }
            else if (!string.IsNullOrEmpty(memo.Text))
            {
                Clipboard.SetText(memo.Text);
            }

            Message.Text = "텍스트가 클립보드에 복사되었습니다.";
        }

        private void 잘라내기ToolStripMenuItem_Click(object sender, EventArgs e)
        {
          
            if (!string.IsNullOrEmpty(memo.SelectedText))
            {
              
                Clipboard.SetText(memo.SelectedText);

                int selectionStart = memo.SelectionStart;
                memo.Text = memo.Text.Remove(selectionStart, memo.SelectionLength);
                memo.SelectionStart = selectionStart;

                Message.Text = "선택된 텍스트가 잘라내기 되었습니다.";
            }
            else if (!string.IsNullOrEmpty(memo.Text))
            {
               
                Clipboard.SetText(memo.Text);
                memo.Clear();

                Message.Text = "전체 텍스트가 잘라내기 되었습니다.";
            }
            else
            {
                Message.Text = "잘라낼 텍스트가 없습니다.";
            }
        }


        private void 붙여넣기ToolStripMenuItem_Click(object sender, EventArgs e)
        {
            
            if (Clipboard.ContainsText())
            {
                int selectionStart = memo.SelectionStart;
                memo.Text = memo.Text.Insert(selectionStart, Clipboard.GetText());

                memo.SelectionStart = selectionStart + Clipboard.GetText().Length;

                Message.Text = "텍스트가 붙여넣기 되었습니다.";
            }
        }

        private void 새탭ToolStripMenuItem_Click(object sender, EventArgs e)
{
            Test_memo newForm = new Test_memo();  
            newForm.Show();
            Message.Text = "";
        }

        private void 확대ToolStripMenuItem1_MouseHover(object sender, EventArgs e)
        {
            Message.Text = "확대 클릭";
        }

        private void 축소ToolStripMenuItem1_MouseHover(object sender, EventArgs e)
        {
            Message.Text = "축소 클릭";
        }

        private void 원래대로돌아가기ToolStripMenuItem_MouseHover(object sender, EventArgs e)
        {
            Message.Text = "원래대로 돌아가기 클릭";
        }

        private void 폰트ToolStripMenuItem_MouseHover(object sender, EventArgs e)
        {
            Message.Text = "폰트 클릭";
        }

        private void 색상ToolStripMenuItem_MouseHover(object sender, EventArgs e)
        {
            Message.Text = "색상 클릭";
        }

        private void 새탭ToolStripMenuItem_MouseMove(object sender, MouseEventArgs e)
        {
            //Message.Text = "새탭 클릭";
        }

        private void openOToolStripMenuItem_MouseHover(object sender, EventArgs e)
        {
            Message.Text = "열기 클릭";
        }

        private void saveSToolStripMenuItem_MouseHover(object sender, EventArgs e)
        {
            Message.Text = "다른 이름으로 저장 클릭";
        }

        private void 복사하기ToolStripMenuItem_MouseHover(object sender, EventArgs e)
        {
            Message.Text = "복사 클릭";
        }

        private void 잘라내기ToolStripMenuItem_MouseHover(object sender, EventArgs e)
        {
            Message.Text = "자르기 클릭";
        }

        private void 붙여넣기ToolStripMenuItem_MouseHover(object sender, EventArgs e)
        {
            Message.Text = "붙여넣기 클릭";
        }

        private void exitEToolStripMenuItem_MouseHover(object sender, EventArgs e)
        {
            Message.Text = "종료 클릭";
        }

        private void 확대ToolStripMenuItem_MouseHover(object sender, EventArgs e)
        {
            Message.Text = "확대/축소 클릭";
        }

        private void file_ba_MouseHover(object sender, EventArgs e)
        {
            Message.Text = "파일 클릭";
        }

        private void typeface_MouseHover(object sender, EventArgs e)
        {
            Message.Text = "글꼴 클릭";
        }

        private void see_MouseHover(object sender, EventArgs e)
        {
            Message.Text = "보기 클릭";
        }

        private void toolStripButton1_Click(object sender, EventArgs e)
        {
            Test_memo newForm = new Test_memo();
            newForm.Show();
            Message.Text = "";
        }

        private void toolStripButton1_MouseHover(object sender, EventArgs e)
        {
            Message.Text = "새탭 열기";
        }

        private void openicon_Click(object sender, EventArgs e)
        {
            openFileDialog1.Filter = "텍스트 문서(*.txt)|*.txt|모든 파일|*.*";
            openFileDialog1.FilterIndex = 1;
            openFileDialog1.InitialDirectory = @"D:\SUUP";
            openFileDialog1.Title = "텍스트 파일 열기";

            if (openFileDialog1.ShowDialog() == DialogResult.OK)
            {
                string File_Name = openFileDialog1.FileName;
                StreamReader str = new StreamReader(File_Name, Encoding.UTF8);
                memo.Text = str.ReadToEnd();
                str.Close();

                _currentFilePath = File_Name; 
            }
        }

        private void saveicon_Click(object sender, EventArgs e)
        {
            saveFileDialog1.Filter = "텍스트 문서(*.txt)|*.txt|모든 파일|*.*";
            saveFileDialog1.OverwritePrompt = true;

            if (saveFileDialog1.ShowDialog() == DialogResult.OK)
            {
                string File_Name = saveFileDialog1.FileName;
                StreamWriter str = new StreamWriter(File_Name, false, Encoding.UTF8);
                str.Write(memo.Text);
                str.Flush();
                str.Close();
            }
        }

        private void anothersaveicon_Click(object sender, EventArgs e)
        {

            if (!string.IsNullOrEmpty(memo.SelectedText))
            {

                Clipboard.SetText(memo.SelectedText);
            }
            else if (!string.IsNullOrEmpty(memo.Text))
            {
                Clipboard.SetText(memo.Text);
            }

            Message.Text = "텍스트가 클립보드에 복사되었습니다.";

        }

        private void cuticon_Click(object sender, EventArgs e)
        {

            if (!string.IsNullOrEmpty(memo.SelectedText))
            {

                Clipboard.SetText(memo.SelectedText);

                int selectionStart = memo.SelectionStart;
                memo.Text = memo.Text.Remove(selectionStart, memo.SelectionLength);
                memo.SelectionStart = selectionStart;

                Message.Text = "선택된 텍스트가 잘라내기 되었습니다.";
            }
            else if (!string.IsNullOrEmpty(memo.Text))
            {
                Clipboard.SetText(memo.Text);
                memo.Clear();
                Message.Text = "전체 텍스트가 잘라내기 되었습니다.";
            }
            else
            {
                Message.Text = "잘라낼 텍스트가 없습니다.";
            }

        }

        private void patcion_Click(object sender, EventArgs e)
        {

            if (Clipboard.ContainsText())
            {
                int selectionStart = memo.SelectionStart;              
                memo.Text = memo.Text.Insert(selectionStart, Clipboard.GetText());
                memo.SelectionStart = selectionStart + Clipboard.GetText().Length;
                Message.Text = "텍스트가 붙여넣기 되었습니다.";
            }

        }

        private void fonticon_Click(object sender, EventArgs e)
        {
            if (fontDialog1.ShowDialog() == DialogResult.OK)
            {
                memo.Font = fontDialog1.Font;
                _originalFont = fontDialog1.Font;
            }

            Message.Text = "";

        }

        private void coloricon_Click(object sender, EventArgs e)
        {

            if (colorDialog1.ShowDialog() == DialogResult.OK)
            {
                memo.ForeColor = colorDialog1.Color;
            }
            Message.Text = "";

        }

        private void inicon_Click(object sender, EventArgs e)
        {

            var currentFont = memo.Font;
            memo.Font = new Font(currentFont.FontFamily, currentFont.Size + 2, currentFont.Style);
            Message.Text = "";

        }

        private void outicon_Click(object sender, EventArgs e)
        {

            var currentFont = memo.Font;
            memo.Font = new Font(currentFont.FontFamily, currentFont.Size - 2, currentFont.Style);
            Message.Text = "";

        }

        private void zoomicon_Click(object sender, EventArgs e)
        {

            memo.Font = _originalFont;
            Message.Text = "";

        }

        private void openicon_MouseHover(object sender, EventArgs e)
        {
            Message.Text = "파일 열기";
        }

        private void saveicon_MouseHover(object sender, EventArgs e)
        {
            Message.Text = "파일 저장";
        }

        private void anothersaveicon_MouseHover(object sender, EventArgs e)
        {
            Message.Text = "다른 이름으로 저장";
        }

        private void cuticon_MouseHover(object sender, EventArgs e)
        {
            Message.Text = "자르기";
        }

        private void patcion_MouseHover(object sender, EventArgs e)
        {
            Message.Text = "붙여넣기";
        }

        private void fonticon_MouseHover(object sender, EventArgs e)
        {
            Message.Text = "폰트 바꾸기";
        }

        private void coloricon_MouseHover(object sender, EventArgs e)
        {
            Message.Text = "색상 바꾸기";
        }

        private void inicon_MouseHover(object sender, EventArgs e)
        {
            Message.Text = "확대하기";
        }

        private void outicon_MouseHover(object sender, EventArgs e)
        {
            Message.Text = "축소하기";
        }

        private void zoomicon_MouseHover(object sender, EventArgs e)
        {
            Message.Text = "화면 원래대로 돌아가기";
        }

        private void 새창AToolStripMenuItem_Click(object sender, EventArgs e)
        {
            
            Test_memo newForm = new Test_memo();
            newForm.ShowDialog(); 
            Message.Text = "";
        }

        private void newcha_MouseHover(object sender, EventArgs e)
        {
            Message.Text = "새창 열기";
        }

        private void toolStripButton1_Click_1(object sender, EventArgs e)
        {
            Test_memo newForm = new Test_memo();
            newForm.ShowDialog(); 
            Message.Text = "";
        }

        private void toolStripButton1_MouseHover_1(object sender, EventArgs e)
        {
            Message.Text = "새창 열기";
        }

        private void newcha_MouseLeave(object sender, EventArgs e)
        {
            Message.Text = "";
        }

        private void file_ba_MouseLeave(object sender, EventArgs e)
        {
            Message.Text = "";
        }

        private void typeface_MouseLeave(object sender, EventArgs e)
        {
            Message.Text = "";
        }

        private void see_MouseLeave(object sender, EventArgs e)
        {
            Message.Text = "";
        }

        private void New_Tab_MouseLeave(object sender, EventArgs e)
        {
            Message.Text = "";
        }

        private void New_Tab_MouseHover(object sender, EventArgs e)
        {
            Message.Text = "새창 열기";
        }

        private void Open_MouseLeave(object sender, EventArgs e)
        {
            Message.Text = "";
        }

        private void Save_MouseLeave(object sender, EventArgs e)
        {
            Message.Text = "";
        }

        private void Copy_MouseLeave(object sender, EventArgs e)
        {
            Message.Text = "";
        }

        private void Cut_MouseLeave(object sender, EventArgs e)
        {
            Message.Text = "";
        }

        private void Paste_MouseLeave(object sender, EventArgs e)
        {
            Message.Text = "";
        }

        private void Exit_MouseLeave(object sender, EventArgs e)
        {
            Message.Text = "";
        }

        private void Font_MouseLeave(object sender, EventArgs e)
        {
            Message.Text = "";
        }

        private void Color_MouseLeave(object sender, EventArgs e)
        {
            Message.Text = "";
        }

        private void ZoomIn_MouseLeave(object sender, EventArgs e)
        {
            Message.Text = "";
        }

        private void ZoomOut_MouseLeave(object sender, EventArgs e)
        {
            Message.Text = "";
        }

        private void ResetZoom_MouseLeave(object sender, EventArgs e)
        {
            Message.Text = "";
        }

        private void toolStripButton1_MouseLeave(object sender, EventArgs e)
        {
            Message.Text = "";
        }

        private void newtabba_MouseLeave(object sender, EventArgs e)
        {
            Message.Text = "";
        }

        private void openicon_MouseLeave(object sender, EventArgs e)
        {
            Message.Text = "";
        }

        private void saveicon_MouseLeave(object sender, EventArgs e)
        {
            Message.Text = "";
        }

        private void anothersaveicon_MouseLeave(object sender, EventArgs e)
        {
            Message.Text = "";
        }

        private void cuticon_MouseLeave(object sender, EventArgs e)
        {
            Message.Text = "";
        }

        private void patcion_MouseLeave(object sender, EventArgs e)
        {
            Message.Text = "";
        }

        private void fonticon_MouseLeave(object sender, EventArgs e)
        {
            Message.Text = "";
        }

        private void coloricon_MouseLeave(object sender, EventArgs e)
        {
            Message.Text = "";
        }

        private void inicon_MouseLeave(object sender, EventArgs e)
        {
            Message.Text = "";
        }

        private void outicon_MouseLeave(object sender, EventArgs e)
        {
            Message.Text = "";
        }

        private void zoomicon_MouseLeave(object sender, EventArgs e)
        {
            Message.Text = "";
        }

        private void 찾기FToolStripMenuItem_Click(object sender, EventArgs e)
        {
            string input = Microsoft.VisualBasic.Interaction.InputBox("찾을 단어를 입력하세요", "찾기");

            if (!string.IsNullOrEmpty(input))
            {
                int index = memo.Text.IndexOf(input);
                if (index >= 0)
                {
                    memo.SelectionStart = index;
                    memo.SelectionLength = input.Length;
                    memo.ScrollToCaret();
                    Message.Text = $"'{input}' 찾음";
                }
                else
                {
                    Message.Text = $"'{input}' 없음";
                }
            }
            Message.Text = "";
        }

        private void 찾기FToolStripMenuItem_MouseHover(object sender, EventArgs e)
        {
            Message.Text = "텍스트 찾기";
        }

        private void 찾기FToolStripMenuItem_MouseLeave(object sender, EventArgs e)
        {
            Message.Text = "";
        }

        

        private void 줄이동JToolStripMenuItem_Click(object sender, EventArgs e)
        {
            string input = Microsoft.VisualBasic.Interaction.InputBox("이동할 줄 번호를 입력하세요", "줄 이동");

            if (int.TryParse(input, out int lineNumber))
            {
                int totalLines = memo.GetLineFromCharIndex(memo.TextLength) + 1;

                if (lineNumber > 0 && lineNumber <= totalLines)
                {
                    int charIndex = memo.GetFirstCharIndexFromLine(lineNumber - 1);
                    memo.SelectionStart = charIndex;
                    memo.SelectionLength = 0;
                    memo.ScrollToCaret();
                    Message.Text = $"{lineNumber}번째 줄로 이동했습니다.";
                }
                else
                {
                    Message.Text = "해당 줄 번호는 범위를 벗어났습니다.";
                }
            }
        }

        private void 줄이동JToolStripMenuItem_MouseHover(object sender, EventArgs e)
        {
            Message.Text = "줄 이동 클릭";
        }

        private void 줄이동JToolStripMenuItem_MouseLeave(object sender, EventArgs e)
        {
            Message.Text = "";
        }

        private void 페이지설정PToolStripMenuItem_Click(object sender, EventArgs e)
        {
            pageSetupDialog1.Document = printDocument1;  
            pageSetupDialog1.ShowDialog();
            Message.Text = "";
        }

        private void 페이지설정PToolStripMenuItem_MouseHover(object sender, EventArgs e)
        {
            Message.Text = "페이지 설정 클릭";
        }

        private void 페이지설정PToolStripMenuItem_MouseLeave(object sender, EventArgs e)
        {
            Message.Text = "";
        }

        private void 인쇄ToolStripMenuItem_Click(object sender, EventArgs e)
        {
            printDialog1.Document = printDocument1;

            if (printDialog1.ShowDialog() == DialogResult.OK)
            {
                printDocument1.Print();
            }
            Message.Text = "";
        }

        private void 인쇄미리보기SToolStripMenuItem_Click(object sender, EventArgs e)
        {
            printPreviewDialog1.Document = printDocument1;
            printPreviewDialog1.ShowDialog();
            Message.Text = "";
        }

        private void 인쇄미리보기SToolStripMenuItem_MouseHover(object sender, EventArgs e)
        {
            Message.Text = "미리보기 클릭";
        }

        private void 인쇄ToolStripMenuItem_MouseHover(object sender, EventArgs e)
        {
            Message.Text = "인쇄 클릭";
        }

        private void 인쇄ToolStripMenuItem_MouseLeave(object sender, EventArgs e)
        {
            Message.Text = "";
        }

        private void 인쇄미리보기SToolStripMenuItem_MouseLeave(object sender, EventArgs e)
        {
            Message.Text = "";
        }

        private void 저장VToolStripMenuItem_Click(object sender, EventArgs e)
        {
            if (!string.IsNullOrEmpty(_currentFilePath))
            {
                StreamWriter writer = new StreamWriter(_currentFilePath, false, Encoding.UTF8);
                writer.Write(memo.Text);
                writer.Close();
            }
            else
            {
                saveSToolStripMenuItem_Click(sender, e);
            }
            Message.Text = "";
        }

        private void 저장VToolStripMenuItem_MouseHover(object sender, EventArgs e)
        {
            Message.Text = "저장 클릭";
        }

        private void 저장VToolStripMenuItem_MouseLeave(object sender, EventArgs e)
        {
            Message.Text = "";
        }

        private void SSAVEICON_Click(object sender, EventArgs e)
        {

            if (!string.IsNullOrEmpty(_currentFilePath))
            {
                StreamWriter writer = new StreamWriter(_currentFilePath, false, Encoding.UTF8);
                writer.Write(memo.Text);
                writer.Close();
            }
            else
            {
                saveSToolStripMenuItem_Click(sender, e);
            }
            Message.Text = "";

        }

        private void SSAVEICON_MouseHover(object sender, EventArgs e)
        {
            Message.Text = "저장 클릭";
        }

        private void SSAVEICON_MouseLeave(object sender, EventArgs e)
        {
            Message.Text = "";
        }

        private void dlsthoicon_Click(object sender, EventArgs e)
        {
            printDialog1.Document = printDocument1;

            if (printDialog1.ShowDialog() == DialogResult.OK)
            {
                printDocument1.Print();
            }
            Message.Text = "";

        }

        private void dlsthoicon_MouseHover(object sender, EventArgs e)
        {
            Message.Text = "인쇄 클릭";
        }

        private void dlsthoicon_MouseLeave(object sender, EventArgs e)
        {
            Message.Text = "";
        }

        private void ALFLQHRLCION_Click(object sender, EventArgs e)
        {
            printPreviewDialog1.Document = printDocument1;
            printPreviewDialog1.ShowDialog();
            Message.Text = "";

        }

        private void ALFLQHRLCION_MouseHover(object sender, EventArgs e)
        {
            Message.Text = "미리보기 클릭";
        }

        private void ALFLQHRLCION_MouseLeave(object sender, EventArgs e)
        {
            Message.Text = "";
        }

        private void FINDICON_Click(object sender, EventArgs e)
        {
            string input = Microsoft.VisualBasic.Interaction.InputBox("찾을 단어를 입력하세요", "찾기");

            if (!string.IsNullOrEmpty(input))
            {
                int index = memo.Text.IndexOf(input);
                if (index >= 0)
                {
                    memo.SelectionStart = index;
                    memo.SelectionLength = input.Length;
                    memo.ScrollToCaret();
                    Message.Text = $"'{input}' 찾음";
                }
                else
                {
                    Message.Text = $"'{input}' 없음";
                }
            }
            Message.Text = "";

        }

        private void FINDICON_MouseHover(object sender, EventArgs e)
        {
            Message.Text = "찾기 클릭";
        }

        private void FINDICON_MouseLeave(object sender, EventArgs e)
        {
            Message.Text = "";
        }

        private void JICON_Click(object sender, EventArgs e)
        {
            string input = Microsoft.VisualBasic.Interaction.InputBox("이동할 줄 번호를 입력하세요", "줄 이동");

            if (int.TryParse(input, out int lineNumber))
            {
                int totalLines = memo.GetLineFromCharIndex(memo.TextLength) + 1;

                if (lineNumber > 0 && lineNumber <= totalLines)
                {
                    int charIndex = memo.GetFirstCharIndexFromLine(lineNumber - 1);
                    memo.SelectionStart = charIndex;
                    memo.SelectionLength = 0;
                    memo.ScrollToCaret();
                    Message.Text = $"{lineNumber}번째 줄로 이동했습니다.";
                }
                else
                {
                    Message.Text = "해당 줄 번호는 범위를 벗어났습니다.";
                }
            }

        }

        private void JICON_MouseHover(object sender, EventArgs e)
        {
            Message.Text = "줄 이동 클릭+";
        }

        private void JICON_MouseLeave(object sender, EventArgs e)
        {
            Message.Text = "";
        }

        private void PAICON_Click(object sender, EventArgs e)
        {
            pageSetupDialog1.Document = printDocument1;
            pageSetupDialog1.ShowDialog();
            Message.Text = "";

        }

        private void PAICON_MouseHover(object sender, EventArgs e)
        {
            Message.Text = "페이지 설정 클릭";
        }

        private void PAICON_MouseLeave(object sender, EventArgs e)
        {
            Message.Text = "";
        }

        private void text_count_Click(object sender, EventArgs e)
        {

        }
        
        private void memo_TextChanged(object sender, EventArgs e)
        {
            int charCount = memo.Text.Length;
            text_count.Text = $"글자 수: {charCount}";
        }
    }
}
