Problem about dates for some company
```
//given a date and a number of days, return the future date


// approach 1: convert date to days, add days, convert back to date
// approach 2: convert addition to date


bool IsLeapYear(int year) {
    if (year % 4 == 0 && year % 100 != 0) {
        return true;
    }
    if (year % 400 == 0) {
        return true;
    }
    return false;
}

std::unordered_map<int, int> month_days = {
    {1, 31},
    {2, 28},
    {3, 31},
    {4, 30},
    {5, 31},
    {6, 30},
    {7, 31},
    {8, 31},
    {9, 30},
    {10, 31},
    {11, 30},
    {12, 31}
};

int ConvertDateToDays(int year, int month, int day) {
    int days = 0;
    for (int i = 1; i < month; i++) {
        days += month_days[i];
    }
    days += day;
    if (IsLeapYear(year) && month > 2) {
        days += 1;
    }
    return days;
}

std::vector<int> ConvertDaysToDate(int days) {
    std::vector<int> date;
    int year = 0;
    int month = 0;
    int day = 0;
    while (days > 0) {
        if (IsLeapYear(year) && month == 2) {
            if (days >= 29) {
                day = 29;
                days -= 29;
            } else {
                day = days;
                days = 0;
            }
        } else {
            if (days >= month_days[month]) {
                day = month_days[month];
                days -= month_days[month];
            } else {
                day = days;
                days = 0;
            }
        }
        month++;
        if (month > 12) {
            month = 1;
            year++;
        }
    }
    date.push_back(year);
    date.push_back(month);
    date.push_back(day);
    return date;
}

std::vector<int> ConvertDateToYearMonthDay(std::string date) {
    std::vector<int> date_vec;
    std::stringstream ss(date);
    std::string token;
    int i = 0;
    while (std::getline(ss, token, '-')) {
        if (i == 0) {
            date_vec.push_back(std::stoi(token));
        } else if (i == 1) {
            date_vec.push_back(std::stoi(token));
        } else {
            date_vec.push_back(std::stoi(token));
        }
        i++;
    }
    return date_vec;
}
```