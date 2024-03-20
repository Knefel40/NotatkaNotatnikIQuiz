# Notatnik

﻿<Window x:Class="Notatnik3A.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:Notatnik3A"
        mc:Ignorable="d"
        Title="MainWindow" Height="450" Width="800">
    <DockPanel>
        <Menu DockPanel.Dock="Top">
            <MenuItem Header="Plik">
                <MenuItem Header="Nowy" Click="MenuItem_Nowy_Click"/>
                <MenuItem Header="Zapisz"/>
                <MenuItem Header="Zapisz jako" Click="MenuItem_Zapiszjako_Click"/>
                <MenuItem Header="Otwórz" Click="MenuItem_Otworz_Click"/>
                <MenuItem Header="Zamknij"/>
            </MenuItem>
            <MenuItem Header="Edycja"></MenuItem>
            <MenuItem Header="Informacje">
                <MenuItem Header="O programie"
                          Click="MenuItem_Oprogramie_Click"
                          />
                <MenuItem Header="O autorze"
                          Click="MenuItem_Oautorze_Click"/>


            </MenuItem>
        </Menu>
        <TextBox x:Name="notatka_textbox"></TextBox>
    </DockPanel>
</Window>




﻿using Microsoft.Win32;
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Imaging;
using System.Windows.Navigation;
using System.Windows.Shapes;

namespace Notatnik3A
{
    /// <summary>
    /// Interaction logic for MainWindow.xaml
    /// </summary>
    public partial class MainWindow : Window
    {
        public MainWindow()
        {
            InitializeComponent();
        }

        private void MenuItem_Oprogramie_Click(object sender, RoutedEventArgs e)
        {
            MessageBox.Show("Notatnik do zapisywania informacji","Informacje o programie");
        }

        private void MenuItem_Oautorze_Click(object sender, RoutedEventArgs e)
        {
            MessageBox.Show("Autorem tego programu jest klasa 3A", "Informacje o autorze");
        }

        private void MenuItem_Nowy_Click(object sender, RoutedEventArgs e)
        {
            notatka_textbox.Text = "";
        }

        private void MenuItem_Otworz_Click(object sender, RoutedEventArgs e)
        {
            var dialog = new OpenFileDialog();
        
            dialog.Filter = "Text documents (.txt)|*.txt";
            dialog.Title = "otwieranie pliku tekstowego";
            dialog.DefaultExt = ".txt";

            if(dialog.ShowDialog() == true)
            {
                string nazwaPliku = dialog.FileName;
                StreamReader plik = new StreamReader(nazwaPliku);
                string text = plik.ReadToEnd();
                plik.Close();
                notatka_textbox.Text = text;

            }
        }

        private void MenuItem_Zapiszjako_Click(object sender, RoutedEventArgs e)
        {
            var dialog = new SaveFileDialog();
            dialog.Filter = "Text documenta(.txt) | *.txt";
            if(dialog.ShowDialog() == true)
            {
                string nazwaPliku = dialog.FileName;
                StreamWriter plik = new StreamWriter(nazwaPliku);
                plik.Write(notatka_textbox.Text);
                plik.Close() ;
            }
        }
    }
}








# Quiz


<Window x:Class="WpfApp3.DodajWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:WpfApp3"
        mc:Ignorable="d"
        Title="DodajWindow" Height="450" Width="800">
    <StackPanel>
        <Label>Podaj Treść Pytania: </Label>
        <TextBox x:Name="TrescPytania"></TextBox>
        <Label>Wybierz poprawną odpowiedz</Label>
        <RadioButton GroupName="odpy" x:Name="Odp_tak" IsChecked="True">Tak</RadioButton>
        <RadioButton GroupName="odpy" x:Name="Odp_nie">Nie</RadioButton>
        <Button Click="Button_Click">Dodaj</Button>
    </StackPanel>
</Window>





using System.Text;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Imaging;
using System.Windows.Navigation;
using System.Windows.Shapes;

namespace WpfApp3
{
    /// <summary>
    /// Interaction logic for MainWindow.xaml
    /// </summary>
    public partial class MainWindow : Window
    {
        public MainWindow()
        {
            InitializeComponent();
        }

        private void Button_Click(object sender, RoutedEventArgs e)
        {
            Window okno = new WykonajWindow();
            //okno.ShowDialog();//okno modalne, nic nie mozna zrobic w tle
            okno.Show(); //okno niemodalne w tle można nadal robić
            Close();
        }

        private void Button_Click_1(object sender, RoutedEventArgs e)
        {
            Window okno = new DodajWindow();
            okno.Show();
            //Close();
        }
    }
}






using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace WpfApp3
{
    public class Pytanie
    {
        public string Tresc {  get; set; }
        public bool Odp { get; set; }

        public Pytanie(string tresc, bool odp)
        {
            Tresc = tresc;
            Odp = odp;
        }
    }
}



Czy Android został zbudowany na podstawie systemu operacyjnego Windows?
nie
Czy WPF to środowisko do aplikacji desktopowych?
tak
Czy Jetpack Compose wykorzystuje język XML?
nie
Czy Angular jest frameworkiem do obsługi baz danych?
nie
Czy karasie jedzą gówno?
nie





using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Imaging;
using System.Windows.Shapes;

namespace WpfApp3
{
    /// <summary>
    /// Logika interakcji dla klasy DodajWindow.xaml
    /// </summary>
    public partial class DodajWindow : Window
    {
        public DodajWindow()
        {
            InitializeComponent();
        }

        private void Button_Click(object sender, RoutedEventArgs e)
        {
            string tresc = TrescPytania.Text;
            string odp;
            if(Odp_tak.IsChecked == true) {
                odp = "tak";
            }
            else
            {
                odp = "nie";
            }
            StreamWriter streamWriter = new StreamWriter("../../../Pytania.txt",true);
            streamWriter.WriteLine(tresc);
            streamWriter.WriteLine(odp);
            streamWriter.Close();
        }
    }
}






<Window x:Class="WpfApp3.DodajWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:WpfApp3"
        mc:Ignorable="d"
        Title="DodajWindow" Height="450" Width="800">
    <StackPanel>
        <Label>Podaj Treść Pytania: </Label>
        <TextBox x:Name="TrescPytania"></TextBox>
        <Label>Wybierz poprawną odpowiedz</Label>
        <RadioButton GroupName="odpy" x:Name="Odp_tak" IsChecked="True">Tak</RadioButton>
        <RadioButton GroupName="odpy" x:Name="Odp_nie">Nie</RadioButton>
        <Button Click="Button_Click">Dodaj</Button>
    </StackPanel>
</Window>
