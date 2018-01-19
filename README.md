# hello-world
first repository 

##GETTING MONTH FROM (MMM DD, YYYY FORMAT)
def getMonthFromDate( date ):
    return(date[:3])
##GETTING YEAR FROM (MMM DD, YYYY FORMAT)
def getYearFromDate( date ):
    return(int(date[8:]))
##GETTING DAY FROM (MMM DD, YYYY FORMAT)
def getDayFromDate(date):
    day = int(date[4:6])
    return day
##DETERMINING LENGTH OF EACH MONTH
def getLengthOfMonth( month , leapYear ):
    if leapYear == False:
        monthLengths = [31, 28,  31,  30, 31,
                        30, 31, 31, 30,  31,
                        30, 31 ]
    else:
        monthLengths = [31, 29,  31,  30, 31,
                        30, 31, 31, 30,  31,
                        30, 31 ]
        
    monthNames = ["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec" ]
    
    monthLength = monthLengths[ monthNames.index(month) ] 
    return monthLength
##DETERMINING IF A YEAR IS A LEAP YEAR
def isLeapYear(year):
    if year % 4 == 0:  #or year%100 == 0:
        if year%100 == 0:
            if year % 400 == 0:
                leapYear = True
            else:
                leapYear = False
        else:
            leapYear = True
    else:
        leapYear = False
    return leapYear
##FINDING NUMBER OF DAYS BETWEEN TWO DATES WITHIN A YEAR
def calculateDaysBetweenWithinYear( month1, day1, year1, month2, day2, year2 ):
    monthNames = ["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec" ]
    leapYear = isLeapYear( year1 )
    numDays = getLengthOfMonth( month1, leapYear ) - day1
    
    monthsBetween = monthNames[ monthNames.index( month1 ) + 1 : monthNames.index( month2 )]
    for month in monthsBetween:
        numDays = numDays + getLengthOfMonth( month, leapYear )
    numDays = numDays + day2
    return numDays
##FINDING NUMBER OF DAYS IN WHOLE YEARS
def calculateDaysInWholeYears(year1, year2):
    numDays = 0
    
    for year in range( year1+1, year2):
        leapYear = isLeapYear( year )
        
        if leapYear == True:
            numDays = numDays + 366
        else:
            numDays = numDays + 365
            
    return numDays
    
##FINDING NUMBER OF DAYS BETWEEN ANY TWO DATES
def calculateDaysBetween( date1, date2):
    month1 = getMonthFromDate( date1 )
    day1 = getDayFromDate( date1 )
    year1 = getYearFromDate( date1 )
    month2 = getMonthFromDate( date2 )
    day2 = getDayFromDate( date2 )
    year2 = getYearFromDate( date2 )
    #IF THE DATES ARE IN THE SAME MONTH OF THE SAME YEAR
    if year1 == year2 and month1 == month2:
        numDays = day2 - day1
    #IF THE DATES ARE IN DIFFERENT MONTHS BUT THE SAME YEAR
    elif year1 == year2:
        numDays = calculateDaysBetweenWithinYear( month1, day1, year1, month2, day2, year2 )
    #IF THE DATES ARE IN DIFFERENT YEARS    
    else:
        #CALCULATING NUMBER OF DAYS IN YEAR1
        numDays = calculateDaysBetweenWithinYear( month1, day1, year1, "Dec", 31, year1 )
        #CALCULATING NUMBER OF DAYS IN THE WHOLE YEAR IN BETWEEN THE TWO DATES
        numDays = numDays + calculateDaysInWholeYears(year1, year2)
       #CALCULATING NUMBER OF DAYS IN YEAR2
        if month2 == "Jan":
            numDays = numDays + day2       
        else:
            numDays = numDays + calculateDaysBetweenWithinYear( "Jan", 1, year2, month2, day2, year2 )
        
   #RETURNING THE NUMBER OF DAYS BETWEEN THE TWO DATES
    return numDays+1 #to include both the starting day and the ending day
