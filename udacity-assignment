import time
import pandas as pd
import numpy as np

CITY_DATA = { 'chicago': 'chicago.csv',
              'new york city': 'new_york_city.csv',
              'washington': 'washington.csv' }

def get_filters():
    """
    Asks user to specify a city, month, and day to analyze.

    Returns:
        (str) city - name of the city to analyze
        (str) month - name of the month to filter by, or "all" to apply no month filter
        (str) day - name of the day of week to filter by, or "all" to apply no day filter
    """
    print('Hello! Let\'s explore some US bikeshare data!')
    # get user input for city (chicago, new york city, washington). HINT: Use a while loop to handle invalid inputs
    city_list = ['chicago', 'new york city', 'washington']


    while True:
        city = input('Would you like to see data for Chicago, New York City, or Washington? ')
        city = city.lower()
        if city in city_list:
            print(city.title())
            break
        else:
            print('There is no existing data about your request.')
        # get user input for month (all, january, february, ... , june)
    month_list = ["all", "january", "february", "march", "april", "may", "june"]

    while True:
        month = input('Please choose a month:  ')
        month = month.lower()

        if month in month_list:
            print(month.title())
            break
        else:
            print("Please choose a valid month. ")
            break

        # get user input for day of week (all, monday, tuesday, ... sunday)
    day_list = ['all', 'monday', 'tuesday', 'wednesday', 'thursday', 'friday', 'saturday', 'sunday']

    while True:
        day = input('Please choose a day of week: ')
        day = day.lower()

        if day in day_list:
            print(day.title())
            break
        else:
            print('Please write a valid day.')


        print('-'*40)
    return city, month, day


def load_data(city, month, day):
    """
    Loads data for the specified city and filters by month and day if applicable.

    Args:
        (str) city - name of the city to analyze
        (str) month - name of the month to filter by, or "all" to apply no month filter
        (str) day - name of the day of week to filter by, or "all" to apply no day filter
    Returns:
        df - Pandas DataFrame containing city data filtered by month and day
    """
    # load data file into a dataframe
    df = pd.read_csv(CITY_DATA[city])

    # convert the Start Time column to datetime
    df['Start Time'] = pd.to_datetime(df['Start Time'])

    # extract month and day of week from Start Time to create new columns
    df['month'] = df['Start Time'].dt.month
    df['day_of_week'] = df['Start Time'].dt.weekday_name


    # filter by month if applicable
    if month != 'all':
        # use the index of the months list to get the corresponding int
        months = ['january', 'february', 'march', 'april', 'may', 'june']
        month = months.index(month) + 1

        # filter by month to create the new dataframe
        df = df[df["month"]==month]


    # filter by day of week if applicable
    if day != 'all':
        # filter by day of week to create the new dataframe
        df = df[df["day_of_week"]==day.title()]


    return df

def time_stats(df):
    """Displays statistics on the most frequent times of travel."""

    print('\nCalculating The Most Frequent Times of Travel...\n')
    start_time = time.time()

    # display the most common month
    months = ['january', 'february', 'march', 'april', 'may', 'june']
    most_common_month = df["month"].mode()[0]
    s=months[most_common_month-1]
    print('The most common month is: ' + s.capitalize())
    # display the most common day of week
    most_common_day = df["day_of_week"].mode()[0]
    print('The most common day is: ' + str(most_common_day))

    # display the most common start hour
    df["hour"] = df["Start Time"].dt.hour
    most_common_hour = df["hour"].mode()[0]
    print('The most common hour is: ' + str(most_common_hour))

    print("\nThis took %s seconds." % (time.time() - start_time))
    print('-'*40)

def station_stats(df):
    """Displays statistics on the most popular stations and trip."""

    print('\nCalculating The Most Popular Stations and Trip...\n')
    start_time = time.time()

    # display most commonly used start station
    print('The most common start station is: ' + df["Start Station"].mode()[0])

    # display most commonly used end station
    print('The most common end station is: ' + df["End Station"].mode()[0])

    # display most frequent combination of start station and end station trip
    df["combination"] = df["Start Station"] + " - " + df["End Station"]
    print('The most frequent combination of start station and end station trip is: ' + df["combination"].mode()[0])

    print("\nThis took %s seconds." % (time.time() - start_time))
    print('-'*40)


def trip_duration_stats(df):
    """Displays statistics on the total and average trip duration."""

    print('\nCalculating Trip Duration...\n')
    start_time = time.time()

    # display total travel time
def trip_duration(df):
    total_duration = df["Trip Duration"].sum()
    print(df["Trip Duration"].sum())
    # display mean travel time
    average_duration = df["Trip Duration"].mean()
    print(df["Trip Duration"].mean())

    print("\nThis took %s seconds." % (time.time() - start_time))
    print('-'*40)


def user_stats(df):
    """Displays statistics on bikeshare users."""

    print('\nCalculating User Stats...\n')
    start_time = time.time()

    # Display counts of user types
    print("Counts of user types: ")
    s=df['User Type'].value_counts()
    print("Subscriber", s[0])
    print("Customer", s[1])
    # Display counts of gender
    if 'Gender' in df.columns:
        print("Counts of gender: ")
        s=df['Gender'].value_counts()
        print("Male", s[0])
        print("Female", s[1])
    else:
        print('oops')
    # Display earliest, most recent, and most common year of birth
    if 'Birth Year' in df.columns:
        s=df["Birth Year"].min()
        print("The youngest users are born in ", int(s))
        s=df["Birth Year"].max()
        print("The oldest users are born in ", int(s))
        s=df["Birth Year"].mode()[0]
        print("The most common birth year among users is ", int(s))

    print("\nThis took %s seconds." % (time.time() - start_time))
    print('-'*40)

def raw_data(df, nline):
    display = input('\nWould you like to display lines from the trip data? Enter yes or no.\n')
    display = display.lower()
    if display == 'yes':
        print(df.iloc[nline:nline+5])
        nline += 5
        return raw_data(df, nline)
    if display == 'no':
        return
    else:
        print("\nPlease try again.")
    return display_data(df, nline)
def main():
    while True:
        city, month, day = get_filters()
        df = load_data(city, month, day)

        time_stats(df)
        station_stats(df)
        trip_duration_stats(df)
        user_stats(df)
        raw_data(df,0)


        restart = input('\nWould you like to restart? Enter yes or no.\n')
        if restart.lower() != 'yes':
            break

if __name__ == "__main__":
	main()
