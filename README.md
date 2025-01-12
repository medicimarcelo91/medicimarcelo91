***SHINNY APP STRUCTURE AND ITS FUNCTIONALITIES***
- Code Comments available and marked with #
  

from shiny import App, render, ui
import matplotlib.pyplot as plt
import seaborn as sns
import pandas as pd

df = pd.read_csv(r'C:\Users\medic\Desktop\College\Data Visualization\2nd Semester Data Visualization\PGdipDataVis2024\CA_Life_Expectancy\expectancy_life_db.csv')

parameters_columns = ['Infant_deaths', 'Under_five_deaths', 'Adult_mortality', 'Alcohol_consumption', 'Hepatitis_B', 'Measles Polio', 'Diphtheria', 'Incidents_HIV', 'GDP_per_capita', 'Population_mln', 'Life_expectancy']

app_ui = ui.page_fluid(
    ui.h1(
        'Global Life Expectancy Overview', style= 'text-align:center;'
    ),
    ui.navset_tab(  
        ui.nav_control(
            ui.input_dark_mode()),   
        ui.nav_panel(
            'Histogram',
            ui.h2(
                'Life Expectancy Comparison'
            ),
            ui.layout_sidebar(
                ui.sidebar(
                    ui.input_selectize(
                    'a',
                    'Select Country1:',
                    {'Afghanistan': 'Afghanistan', 'Albania': 'Albania', 'Algeria': 'Algeria', 'Angola': 'Angola', 'Antigua and Barbuda': 'Antigua and Barbuda', 'Argentina': 'Argentina', 'Armenia': 'Armenia', 'Australia': 'Australia', 'Austria': 'Austria', 'Azerbaijan': 'Azerbaijan', 'Bahamas, The': 'Bahamas, The', 'Bahrain': 'Bahrain', 'Bangladesh': 'Bangladesh', 'Barbados': 'Barbados', 'Belarus': 'Belarus', 'Belgium': 'Belgium', 'Belize': 'Belize', 'Benin': 'Benin', 'Bhutan': 'Bhutan', 'Bolivia': 'Bolivia', 'Bosnia and Herzegovina': 'Bosnia and Herzegovina', 'Botswana': 'Botswana', 'Brazil': 'Brazil', 'Brunei Darussalam': 'Brunei Darussalam', 'Bulgaria': 'Bulgaria', 'Burkina Faso': 'Burkina Faso', 'Burundi': 'Burundi', 'Cabo Verde': 'Cabo Verde', 'Cambodia': 'Cambodia', 'Cameroon': 'Cameroon', 'Canada': 'Canada', 'Central African Republic': 'Central African Republic', 'Chad': 'Chad', 'Chile': 'Chile', 'China': 'China', 'Colombia': 'Colombia', 'Comoros': 'Comoros', 'Congo, Dem. Rep.': 'Congo, Dem. Rep.', 'Congo, Rep.': 'Congo, Rep.', 'Costa Rica': 'Costa Rica', "Cote d'Ivoire": "Cote d'Ivoire", 'Croatia': 'Croatia', 'Cuba': 'Cuba', 'Cyprus': 'Cyprus', 'Czechia': 'Czechia', 'Denmark': 'Denmark', 'Djibouti': 'Djibouti', 'Dominican Republic': 'Dominican Republic', 'Ecuador': 'Ecuador', 'Egypt, Arab Rep.': 'Egypt, Arab Rep.', 'El Salvador': 'El Salvador', 'Equatorial Guinea': 'Equatorial Guinea', 'Eritrea': 'Eritrea', 'Estonia': 'Estonia', 'Eswatini': 'Eswatini', 'Ethiopia': 'Ethiopia', 'Fiji': 'Fiji', 'Finland': 'Finland', 'France': 'France', 'Gabon': 'Gabon', 'Gambia, The': 'Gambia, The', 'Georgia': 'Georgia', 'Germany': 'Germany', 'Ghana': 'Ghana', 'Greece': 'Greece', 'Grenada': 'Grenada', 'Guatemala': 'Guatemala', 'Guinea': 'Guinea', 'Guinea-Bissau': 'Guinea-Bissau', 'Guyana': 'Guyana', 'Haiti': 'Haiti', 'Honduras': 'Honduras', 'Hungary': 'Hungary', 'Iceland': 'Iceland', 'India': 'India', 'Indonesia': 'Indonesia', 'Iran, Islamic Rep.': 'Iran, Islamic Rep.', 'Iraq': 'Iraq', 'Ireland': 'Ireland', 'Israel': 'Israel', 'Italy': 'Italy', 'Jamaica': 'Jamaica', 'Japan': 'Japan', 'Jordan': 'Jordan', 'Kazakhstan': 'Kazakhstan', 'Kenya': 'Kenya', 'Kiribati': 'Kiribati', 'Kuwait': 'Kuwait', 'Kyrgyz Republic': 'Kyrgyz Republic', 'Lao PDR': 'Lao PDR', 'Latvia': 'Latvia', 'Lebanon': 'Lebanon', 'Lesotho': 'Lesotho', 'Liberia': 'Liberia', 'Libya': 'Libya', 'Lithuania': 'Lithuania', 'Luxembourg': 'Luxembourg', 'Madagascar': 'Madagascar', 'Malawi': 'Malawi', 'Malaysia': 'Malaysia', 'Maldives': 'Maldives', 'Mali': 'Mali', 'Malta': 'Malta', 'Mauritania': 'Mauritania', 'Mauritius': 'Mauritius', 'Mexico': 'Mexico', 'Micronesia, Fed. Sts.': 'Micronesia, Fed. Sts.', 'Moldova': 'Moldova', 'Mongolia': 'Mongolia', 'Montenegro': 'Montenegro', 'Morocco': 'Morocco', 'Mozambique': 'Mozambique', 'Myanmar': 'Myanmar', 'Namibia': 'Namibia', 'Nepal': 'Nepal', 'Netherlands': 'Netherlands', 'New Zealand': 'New Zealand', 'Nicaragua': 'Nicaragua', 'Niger': 'Niger', 'Nigeria': 'Nigeria', 'North Macedonia': 'North Macedonia', 'Norway': 'Norway', 'Oman': 'Oman', 'Pakistan': 'Pakistan', 'Panama': 'Panama', 'Papua New Guinea': 'Papua New Guinea', 'Paraguay': 'Paraguay', 'Peru': 'Peru', 'Philippines': 'Philippines', 'Poland': 'Poland', 'Portugal': 'Portugal', 'Qatar': 'Qatar', 'Romania': 'Romania', 'Russian Federation': 'Russian Federation', 'Rwanda': 'Rwanda', 'Samoa': 'Samoa', 'Sao Tome and Principe': 'Sao Tome and Principe', 'Saudi Arabia': 'Saudi Arabia', 'Senegal': 'Senegal', 'Serbia': 'Serbia', 'Seychelles': 'Seychelles', 'Sierra Leone': 'Sierra Leone', 'Singapore': 'Singapore', 'Slovak Republic': 'Slovak Republic', 'Slovenia': 'Slovenia', 'Solomon Islands': 'Solomon Islands', 'Somalia': 'Somalia', 'South Africa': 'South Africa', 'Spain': 'Spain', 'Sri Lanka': 'Sri Lanka', 'St. Lucia': 'St. Lucia', 'St. Vincent and the Grenadines': 'St. Vincent and the Grenadines', 'Suriname': 'Suriname', 'Sweden': 'Sweden', 'Switzerland': 'Switzerland', 'Syrian Arab Republic': 'Syrian Arab Republic', 'Tajikistan': 'Tajikistan', 'Tanzania': 'Tanzania', 'Thailand': 'Thailand', 'Timor-Leste': 'Timor-Leste', 'Togo': 'Togo', 'Tonga': 'Tonga', 'Trinidad and Tobago': 'Trinidad and Tobago', 'Tunisia': 'Tunisia', 'Turkiye': 'Turkiye', 'Turkmenistan': 'Turkmenistan', 'Uganda': 'Uganda', 'Ukraine': 'Ukraine', 'United Arab Emirates': 'United Arab Emirates', 'United Kingdom': 'United Kingdom', 'United States': 'United States', 'Uruguay': 'Uruguay', 'Uzbekistan': 'Uzbekistan', 'Vanuatu': 'Vanuatu', 'Venezuela, RB': 'Venezuela, RB', 'Vietnam': 'Vietnam', 'Yemen, Rep.': 'Yemen, Rep.', 'Zambia': 'Zambia', 'Zimbabwe': 'Zimbabwe'},
                    multiple=False,
                    ),
                    ui.input_selectize(
                    'b',
                    'Select Country2:',
                    {'Afghanistan': 'Afghanistan', 'Albania': 'Albania', 'Algeria': 'Algeria', 'Angola': 'Angola', 'Antigua and Barbuda': 'Antigua and Barbuda', 'Argentina': 'Argentina', 'Armenia': 'Armenia', 'Australia': 'Australia', 'Austria': 'Austria', 'Azerbaijan': 'Azerbaijan', 'Bahamas, The': 'Bahamas, The', 'Bahrain': 'Bahrain', 'Bangladesh': 'Bangladesh', 'Barbados': 'Barbados', 'Belarus': 'Belarus', 'Belgium': 'Belgium', 'Belize': 'Belize', 'Benin': 'Benin', 'Bhutan': 'Bhutan', 'Bolivia': 'Bolivia', 'Bosnia and Herzegovina': 'Bosnia and Herzegovina', 'Botswana': 'Botswana', 'Brazil': 'Brazil', 'Brunei Darussalam': 'Brunei Darussalam', 'Bulgaria': 'Bulgaria', 'Burkina Faso': 'Burkina Faso', 'Burundi': 'Burundi', 'Cabo Verde': 'Cabo Verde', 'Cambodia': 'Cambodia', 'Cameroon': 'Cameroon', 'Canada': 'Canada', 'Central African Republic': 'Central African Republic', 'Chad': 'Chad', 'Chile': 'Chile', 'China': 'China', 'Colombia': 'Colombia', 'Comoros': 'Comoros', 'Congo, Dem. Rep.': 'Congo, Dem. Rep.', 'Congo, Rep.': 'Congo, Rep.', 'Costa Rica': 'Costa Rica', "Cote d'Ivoire": "Cote d'Ivoire", 'Croatia': 'Croatia', 'Cuba': 'Cuba', 'Cyprus': 'Cyprus', 'Czechia': 'Czechia', 'Denmark': 'Denmark', 'Djibouti': 'Djibouti', 'Dominican Republic': 'Dominican Republic', 'Ecuador': 'Ecuador', 'Egypt, Arab Rep.': 'Egypt, Arab Rep.', 'El Salvador': 'El Salvador', 'Equatorial Guinea': 'Equatorial Guinea', 'Eritrea': 'Eritrea', 'Estonia': 'Estonia', 'Eswatini': 'Eswatini', 'Ethiopia': 'Ethiopia', 'Fiji': 'Fiji', 'Finland': 'Finland', 'France': 'France', 'Gabon': 'Gabon', 'Gambia, The': 'Gambia, The', 'Georgia': 'Georgia', 'Germany': 'Germany', 'Ghana': 'Ghana', 'Greece': 'Greece', 'Grenada': 'Grenada', 'Guatemala': 'Guatemala', 'Guinea': 'Guinea', 'Guinea-Bissau': 'Guinea-Bissau', 'Guyana': 'Guyana', 'Haiti': 'Haiti', 'Honduras': 'Honduras', 'Hungary': 'Hungary', 'Iceland': 'Iceland', 'India': 'India', 'Indonesia': 'Indonesia', 'Iran, Islamic Rep.': 'Iran, Islamic Rep.', 'Iraq': 'Iraq', 'Ireland': 'Ireland', 'Israel': 'Israel', 'Italy': 'Italy', 'Jamaica': 'Jamaica', 'Japan': 'Japan', 'Jordan': 'Jordan', 'Kazakhstan': 'Kazakhstan', 'Kenya': 'Kenya', 'Kiribati': 'Kiribati', 'Kuwait': 'Kuwait', 'Kyrgyz Republic': 'Kyrgyz Republic', 'Lao PDR': 'Lao PDR', 'Latvia': 'Latvia', 'Lebanon': 'Lebanon', 'Lesotho': 'Lesotho', 'Liberia': 'Liberia', 'Libya': 'Libya', 'Lithuania': 'Lithuania', 'Luxembourg': 'Luxembourg', 'Madagascar': 'Madagascar', 'Malawi': 'Malawi', 'Malaysia': 'Malaysia', 'Maldives': 'Maldives', 'Mali': 'Mali', 'Malta': 'Malta', 'Mauritania': 'Mauritania', 'Mauritius': 'Mauritius', 'Mexico': 'Mexico', 'Micronesia, Fed. Sts.': 'Micronesia, Fed. Sts.', 'Moldova': 'Moldova', 'Mongolia': 'Mongolia', 'Montenegro': 'Montenegro', 'Morocco': 'Morocco', 'Mozambique': 'Mozambique', 'Myanmar': 'Myanmar', 'Namibia': 'Namibia', 'Nepal': 'Nepal', 'Netherlands': 'Netherlands', 'New Zealand': 'New Zealand', 'Nicaragua': 'Nicaragua', 'Niger': 'Niger', 'Nigeria': 'Nigeria', 'North Macedonia': 'North Macedonia', 'Norway': 'Norway', 'Oman': 'Oman', 'Pakistan': 'Pakistan', 'Panama': 'Panama', 'Papua New Guinea': 'Papua New Guinea', 'Paraguay': 'Paraguay', 'Peru': 'Peru', 'Philippines': 'Philippines', 'Poland': 'Poland', 'Portugal': 'Portugal', 'Qatar': 'Qatar', 'Romania': 'Romania', 'Russian Federation': 'Russian Federation', 'Rwanda': 'Rwanda', 'Samoa': 'Samoa', 'Sao Tome and Principe': 'Sao Tome and Principe', 'Saudi Arabia': 'Saudi Arabia', 'Senegal': 'Senegal', 'Serbia': 'Serbia', 'Seychelles': 'Seychelles', 'Sierra Leone': 'Sierra Leone', 'Singapore': 'Singapore', 'Slovak Republic': 'Slovak Republic', 'Slovenia': 'Slovenia', 'Solomon Islands': 'Solomon Islands', 'Somalia': 'Somalia', 'South Africa': 'South Africa', 'Spain': 'Spain', 'Sri Lanka': 'Sri Lanka', 'St. Lucia': 'St. Lucia', 'St. Vincent and the Grenadines': 'St. Vincent and the Grenadines', 'Suriname': 'Suriname', 'Sweden': 'Sweden', 'Switzerland': 'Switzerland', 'Syrian Arab Republic': 'Syrian Arab Republic', 'Tajikistan': 'Tajikistan', 'Tanzania': 'Tanzania', 'Thailand': 'Thailand', 'Timor-Leste': 'Timor-Leste', 'Togo': 'Togo', 'Tonga': 'Tonga', 'Trinidad and Tobago': 'Trinidad and Tobago', 'Tunisia': 'Tunisia', 'Turkiye': 'Turkiye', 'Turkmenistan': 'Turkmenistan', 'Uganda': 'Uganda', 'Ukraine': 'Ukraine', 'United Arab Emirates': 'United Arab Emirates', 'United Kingdom': 'United Kingdom', 'United States': 'United States', 'Uruguay': 'Uruguay', 'Uzbekistan': 'Uzbekistan', 'Vanuatu': 'Vanuatu', 'Venezuela, RB': 'Venezuela, RB', 'Vietnam': 'Vietnam', 'Yemen, Rep.': 'Yemen, Rep.', 'Zambia': 'Zambia', 'Zimbabwe': 'Zimbabwe'},
                    multiple=False,
                    ),
                ),
                ui.output_plot('histogram'),
            ),
        ),
        ui.nav_panel(
            'Scatterplot',
            ui.layout_sidebar(
                ui.sidebar(
                    ui.input_selectize(
                    'c',
                    'Select Country:',
                    {'Afghanistan': 'Afghanistan', 'Albania': 'Albania', 'Algeria': 'Algeria', 'Angola': 'Angola', 'Antigua and Barbuda': 'Antigua and Barbuda', 'Argentina': 'Argentina', 'Armenia': 'Armenia', 'Australia': 'Australia', 'Austria': 'Austria', 'Azerbaijan': 'Azerbaijan', 'Bahamas, The': 'Bahamas, The', 'Bahrain': 'Bahrain', 'Bangladesh': 'Bangladesh', 'Barbados': 'Barbados', 'Belarus': 'Belarus', 'Belgium': 'Belgium', 'Belize': 'Belize', 'Benin': 'Benin', 'Bhutan': 'Bhutan', 'Bolivia': 'Bolivia', 'Bosnia and Herzegovina': 'Bosnia and Herzegovina', 'Botswana': 'Botswana', 'Brazil': 'Brazil', 'Brunei Darussalam': 'Brunei Darussalam', 'Bulgaria': 'Bulgaria', 'Burkina Faso': 'Burkina Faso', 'Burundi': 'Burundi', 'Cabo Verde': 'Cabo Verde', 'Cambodia': 'Cambodia', 'Cameroon': 'Cameroon', 'Canada': 'Canada', 'Central African Republic': 'Central African Republic', 'Chad': 'Chad', 'Chile': 'Chile', 'China': 'China', 'Colombia': 'Colombia', 'Comoros': 'Comoros', 'Congo, Dem. Rep.': 'Congo, Dem. Rep.', 'Congo, Rep.': 'Congo, Rep.', 'Costa Rica': 'Costa Rica', "Cote d'Ivoire": "Cote d'Ivoire", 'Croatia': 'Croatia', 'Cuba': 'Cuba', 'Cyprus': 'Cyprus', 'Czechia': 'Czechia', 'Denmark': 'Denmark', 'Djibouti': 'Djibouti', 'Dominican Republic': 'Dominican Republic', 'Ecuador': 'Ecuador', 'Egypt, Arab Rep.': 'Egypt, Arab Rep.', 'El Salvador': 'El Salvador', 'Equatorial Guinea': 'Equatorial Guinea', 'Eritrea': 'Eritrea', 'Estonia': 'Estonia', 'Eswatini': 'Eswatini', 'Ethiopia': 'Ethiopia', 'Fiji': 'Fiji', 'Finland': 'Finland', 'France': 'France', 'Gabon': 'Gabon', 'Gambia, The': 'Gambia, The', 'Georgia': 'Georgia', 'Germany': 'Germany', 'Ghana': 'Ghana', 'Greece': 'Greece', 'Grenada': 'Grenada', 'Guatemala': 'Guatemala', 'Guinea': 'Guinea', 'Guinea-Bissau': 'Guinea-Bissau', 'Guyana': 'Guyana', 'Haiti': 'Haiti', 'Honduras': 'Honduras', 'Hungary': 'Hungary', 'Iceland': 'Iceland', 'India': 'India', 'Indonesia': 'Indonesia', 'Iran, Islamic Rep.': 'Iran, Islamic Rep.', 'Iraq': 'Iraq', 'Ireland': 'Ireland', 'Israel': 'Israel', 'Italy': 'Italy', 'Jamaica': 'Jamaica', 'Japan': 'Japan', 'Jordan': 'Jordan', 'Kazakhstan': 'Kazakhstan', 'Kenya': 'Kenya', 'Kiribati': 'Kiribati', 'Kuwait': 'Kuwait', 'Kyrgyz Republic': 'Kyrgyz Republic', 'Lao PDR': 'Lao PDR', 'Latvia': 'Latvia', 'Lebanon': 'Lebanon', 'Lesotho': 'Lesotho', 'Liberia': 'Liberia', 'Libya': 'Libya', 'Lithuania': 'Lithuania', 'Luxembourg': 'Luxembourg', 'Madagascar': 'Madagascar', 'Malawi': 'Malawi', 'Malaysia': 'Malaysia', 'Maldives': 'Maldives', 'Mali': 'Mali', 'Malta': 'Malta', 'Mauritania': 'Mauritania', 'Mauritius': 'Mauritius', 'Mexico': 'Mexico', 'Micronesia, Fed. Sts.': 'Micronesia, Fed. Sts.', 'Moldova': 'Moldova', 'Mongolia': 'Mongolia', 'Montenegro': 'Montenegro', 'Morocco': 'Morocco', 'Mozambique': 'Mozambique', 'Myanmar': 'Myanmar', 'Namibia': 'Namibia', 'Nepal': 'Nepal', 'Netherlands': 'Netherlands', 'New Zealand': 'New Zealand', 'Nicaragua': 'Nicaragua', 'Niger': 'Niger', 'Nigeria': 'Nigeria', 'North Macedonia': 'North Macedonia', 'Norway': 'Norway', 'Oman': 'Oman', 'Pakistan': 'Pakistan', 'Panama': 'Panama', 'Papua New Guinea': 'Papua New Guinea', 'Paraguay': 'Paraguay', 'Peru': 'Peru', 'Philippines': 'Philippines', 'Poland': 'Poland', 'Portugal': 'Portugal', 'Qatar': 'Qatar', 'Romania': 'Romania', 'Russian Federation': 'Russian Federation', 'Rwanda': 'Rwanda', 'Samoa': 'Samoa', 'Sao Tome and Principe': 'Sao Tome and Principe', 'Saudi Arabia': 'Saudi Arabia', 'Senegal': 'Senegal', 'Serbia': 'Serbia', 'Seychelles': 'Seychelles', 'Sierra Leone': 'Sierra Leone', 'Singapore': 'Singapore', 'Slovak Republic': 'Slovak Republic', 'Slovenia': 'Slovenia', 'Solomon Islands': 'Solomon Islands', 'Somalia': 'Somalia', 'South Africa': 'South Africa', 'Spain': 'Spain', 'Sri Lanka': 'Sri Lanka', 'St. Lucia': 'St. Lucia', 'St. Vincent and the Grenadines': 'St. Vincent and the Grenadines', 'Suriname': 'Suriname', 'Sweden': 'Sweden', 'Switzerland': 'Switzerland', 'Syrian Arab Republic': 'Syrian Arab Republic', 'Tajikistan': 'Tajikistan', 'Tanzania': 'Tanzania', 'Thailand': 'Thailand', 'Timor-Leste': 'Timor-Leste', 'Togo': 'Togo', 'Tonga': 'Tonga', 'Trinidad and Tobago': 'Trinidad and Tobago', 'Tunisia': 'Tunisia', 'Turkiye': 'Turkiye', 'Turkmenistan': 'Turkmenistan', 'Uganda': 'Uganda', 'Ukraine': 'Ukraine', 'United Arab Emirates': 'United Arab Emirates', 'United Kingdom': 'United Kingdom', 'United States': 'United States', 'Uruguay': 'Uruguay', 'Uzbekistan': 'Uzbekistan', 'Vanuatu': 'Vanuatu', 'Venezuela, RB': 'Venezuela, RB', 'Vietnam': 'Vietnam', 'Yemen, Rep.': 'Yemen, Rep.', 'Zambia': 'Zambia', 'Zimbabwe': 'Zimbabwe'},
                    multiple=True,
                    ),
                ),
                ui.output_plot('graph')
            ),
        ),
        ui.nav_panel(
            'Data Frame',
            ui.layout_sidebar(
                ui.sidebar(
                    ui.input_slider(
                        'g',
                        'Select Range',min=1,max=100,value=[25,50]
                    ),
                ),
                ui.output_data_frame('Data_Frame')
            ),
        ),
                
    ),
)

def server(input, output, session):
    @output
    @render.plot
    def histogram():
        Parameter1 = df[df['Country'] == input.a()]
        Parameter2 = df[df['Country'] == input.b()]

        plt.bar(Parameter1['Country'], Parameter1['Life_expectancy'], color='skyblue')
        plt.bar(Parameter2['Country'], Parameter2['Life_expectancy'], color='grey')
        plt.xlabel('Country')
        plt.ylabel('Life_expectancy')
        return plt.gcf()  
               
    @output
    @render.plot
    def graph():
        input1 = input.c() or []

        if input1:
            filtered_data = df[
                (df['Country'].isin(input1))
            ]
            plt.figure()
            sns.scatterplot(
                data=filtered_data,
                x='Life_expectancy',
                y='GDP_per_capita',  
                hue='Country',
            )
            plt.title('Life Expectancy vs GDP Per Capita')
            plt.xlabel('Life Expectancy')
            plt.ylabel('GDP per Capita')
            return plt.gcf()
    
    @render.data_frame
    def Data_Frame():
        input_range = input.g()
        selected_data = df[(df['Life_expectancy'] >= input_range[0]) & (df['Life_expectancy'] <= input_range[1])]
        return render.DataGrid(selected_data)

app = App(app_ui, server)




