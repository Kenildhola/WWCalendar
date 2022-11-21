# WWCalendar

    var isStartDate = false
    
    fileprivate var singleDate: Date = Date()
    fileprivate var multipleDates: [Date] = []
    
    // Action
    
     @IBAction func clickedFromDate(_ sender: Any) {
        
        self.view.endEditing(true)
        
        isStartDate = true
        
        let FromDate = UIStoryboard(name: "WWCalendarTimeSelector", bundle: nil).instantiateInitialViewController() as! WWCalendarTimeSelector
        FromDate.delegate = self
        FromDate.optionCurrentDate = singleDate
        FromDate.optionCurrentDates = Set(multipleDates)
        FromDate.optionCurrentDateRange.setStartDate(multipleDates.first ?? singleDate)
        FromDate.optionCurrentDateRange.setEndDate(multipleDates.last ?? singleDate)
        
        FromDate.optionStyles.showDateMonth(true)
        FromDate.optionStyles.showMonth(false)
        FromDate.optionStyles.showYear(true)
        FromDate.optionStyles.showTime(false)
        
        present(FromDate, animated: true, completion: nil)
        
        
    }
    @IBAction func clickedToDate(_ sender: Any) {
        
        self.view.endEditing(true)
        
        isStartDate = false
        
        let ToDate = UIStoryboard(name: "WWCalendarTimeSelector", bundle: nil).instantiateInitialViewController() as! WWCalendarTimeSelector
        ToDate.delegate = self
        ToDate.optionCurrentDate = singleDate
        ToDate.optionCurrentDates = Set(multipleDates)
        ToDate.optionCurrentDateRange.setStartDate(multipleDates.first ?? singleDate)
        ToDate.optionCurrentDateRange.setEndDate(multipleDates.last ?? singleDate)
        
        ToDate.optionStyles.showDateMonth(true)
        ToDate.optionStyles.showMonth(false)
        ToDate.optionStyles.showYear(true)
        ToDate.optionStyles.showTime(false)
        
        
        present(ToDate, animated: true, completion: nil)
        
    }
    
    
    // delegate
    
    extension AdminHomeworkReportVC: WWCalendarTimeSelectorProtocol
{
    func WWCalendarTimeSelectorDone(_ selector: WWCalendarTimeSelector, date: Date) {
        print("Selected \n\(date)\n---")
        singleDate = date
        
        if isStartDate == true
        {
            txtFromDate.text = date.stringFromFormat("dd-MM-yyyy")
        }
        else
        {
            txtToDate.text = date.stringFromFormat("dd-MM-yyyy")
        }
        
    }
    
    func AdminHomeworkReportVC(_ selector: WWCalendarTimeSelector, dates: [Date]) {
        print("Selected Multiple Dates \n\(dates)\n---")
      
        if isStartDate == true
        {
            if let Fromdate = dates.first {
                singleDate = Fromdate
                txtFromDate.text = Fromdate.stringFromFormat("dd-MM-yyyy")
            }
            else {
                txtFromDate.text = "No Date Selected"
            }
        }
        else
        {
            if let Todate = dates.first {
                singleDate = Todate
                txtToDate.text = Todate.stringFromFormat("dd-MM-yyyy")
            }
            else {
                txtToDate.text = "No Date Selected"
            }
        }
       
        multipleDates = dates
    }
}
