# PMS Software - Visual Flowcharts & Diagrams
## Interactive User Flow Diagrams

> **Note**: These diagrams use Mermaid syntax and will render as interactive flowcharts in GitHub, GitLab, VS Code (with Mermaid extension), and many documentation tools.

---

## 📊 Table of Contents
1. [System Authentication Flow](#system-authentication-flow)
2. [Admin Complete Flow](#admin-complete-flow)
3. [Front Desk User Flow](#front-desk-user-flow)
4. [Housekeeping User Flow](#housekeeping-user-flow)
5. [Reservation Management Flow](#reservation-management-flow)
6. [Billing & Payment Flow](#billing--payment-flow)
7. [Magic Link Flow](#magic-link-flow)
8. [Housekeeping Operations Flow](#housekeeping-operations-flow)
9. [Guest Check-in Journey](#guest-check-in-journey)
10. [Guest Check-out Journey](#guest-check-out-journey)

---

## 1. System Authentication Flow

```mermaid
graph TD
    Start([User Opens PMS]) --> Login[Login Page]
    Login --> Auth{Authenticate User}
    Auth -->|Invalid| Error[Show Error Message]
    Error --> Login
    Auth -->|Valid Admin| AdminDash[Admin Dashboard]
    Auth -->|Valid Front Desk| FrontDeskDash[Front Desk Dashboard]
    Auth -->|Valid Housekeeping| HousekeepingDash[Housekeeping Dashboard]
    
    AdminDash --> AdminModules[All Modules Access]
    FrontDeskDash --> FDModules[Limited Modules Access]
    HousekeepingDash --> HKModules[Housekeeping Only]
    
    style AdminDash fill:#2ecc71
    style FrontDeskDash fill:#3498db
    style HousekeepingDash fill:#e74c3c
    style Auth fill:#f39c12
```

---

## 2. Admin Complete Flow

```mermaid
graph TB
    Admin([Admin User]) --> Dashboard[Admin Dashboard]
    
    Dashboard --> Reservation[Reservation Management]
    Dashboard --> Billing[Billing & Payments]
    Dashboard --> Housekeeping[Housekeeping]
    Dashboard --> MagicLink[Magic Link]
    Dashboard --> CRM[CRM & Chat]
    Dashboard --> Reports[Reports & Analytics]
    Dashboard --> Settings[Settings & Config]
    Dashboard --> Users[User Management]
    
    Reservation --> R1[View Calendar]
    Reservation --> R2[Create Booking]
    Reservation --> R3[Modify Booking]
    Reservation --> R4[Cancel Booking]
    
    Billing --> B1[View Folio]
    Billing --> B2[Process Payment]
    Billing --> B3[Generate Receipt]
    Billing --> B4[Apply Discounts]
    
    Housekeeping --> H1[View Room Status]
    Housekeeping --> H2[Assign Staff]
    Housekeeping --> H3[Update Status]
    Housekeeping --> H4[Export Reports]
    
    MagicLink --> M1[Generate Link]
    MagicLink --> M2[Send to Guest]
    MagicLink --> M3[Track Activity]
    
    CRM --> C1[View Messages]
    CRM --> C2[Reply to Guests]
    CRM --> C3[Booking.com Integration]
    CRM --> C4[Airbnb Integration]
    
    Settings --> S1[Property Settings]
    Settings --> S2[Rate Plans]
    Settings --> S3[Room Types]
    Settings --> S4[Tax Configuration]
    
    Users --> U1[Add Users]
    Users --> U2[Manage Roles]
    Users --> U3[Set Permissions]
    
    style Admin fill:#2ecc71
    style Dashboard fill:#3498db
    style Reservation fill:#e67e22
    style Billing fill:#9b59b6
    style Housekeeping fill:#e74c3c
    style MagicLink fill:#1abc9c
    style CRM fill:#34495e
    style Settings fill:#95a5a6
    style Users fill:#16a085
```

---

## 3. Front Desk User Flow

```mermaid
graph TB
    FD([Front Desk User]) --> FDDash[Front Desk Dashboard]
    
    FDDash --> FDRes[Reservation Management]
    FDDash --> FDBill[Billing & Payments]
    FDDash --> FDHouse[Housekeeping View]
    FDDash --> FDMagic[Magic Link]
    
    FDRes --> FDR1[Search Reservation]
    FDRes --> FDR2[Create Booking]
    FDRes --> FDR3[Check-in Guest]
    FDRes --> FDR4[Check-out Guest]
    FDRes --> FDR5[Modify Booking]
    FDRes --> FDR6[Assign Room]
    
    FDBill --> FDB1[View Guest Folio]
    FDBill --> FDB2[Collect Payment]
    FDBill --> FDB3[Print Receipt]
    FDBill --> FDB4[Split Bill]
    FDBill --> FDB5[Apply Discount]
    
    FDHouse --> FDH1[View Room Status]
    FDHouse --> FDH2[Check Availability]
    FDHouse --> FDH3[View Cleaning Status]
    
    FDMagic --> FDM1[Generate Magic Link]
    FDMagic --> FDM2[Send via Email/SMS]
    FDMagic --> FDM3[Resend Link]
    
    FDR3 --> CheckIn{Guest Present?}
    CheckIn -->|Yes| CI1[Verify ID]
    CI1 --> CI2[Collect Payment]
    CI2 --> CI3[Assign Room]
    CI3 --> CI4[Print Reg Card]
    CI4 --> CI5[Provide Key]
    CI5 --> CI6[Complete Check-in]
    
    FDR4 --> CheckOut{Ready to Checkout?}
    CheckOut -->|Yes| CO1[Review Charges]
    CO1 --> CO2[Settle Balance]
    CO2 --> CO3[Print Receipt]
    CO3 --> CO4[Mark Checkout]
    CO4 --> CO5[Update Room Status]
    
    style FD fill:#3498db
    style FDDash fill:#5dade2
    style CheckIn fill:#f39c12
    style CheckOut fill:#e67e22
```

---

## 4. Housekeeping User Flow

```mermaid
graph TB
    HK([Housekeeping User]) --> HKDash[Housekeeping Dashboard]
    
    HKDash --> ViewType{Select View Type}
    ViewType -->|List View| ListView[Table View with All Rooms]
    ViewType -->|Grid View| GridView[Card View with Room Status]
    
    ListView --> LV1[See Room Number]
    ListView --> LV2[See Room Type]
    ListView --> LV3[See Current Status]
    ListView --> LV4[See Assigned Staff]
    ListView --> LV5[Filter by Status]
    
    GridView --> GV1[Select Staff]
    GridView --> GV2[Select Room Type]
    GridView --> GV3[View Room Cards]
    
    LV3 --> Status{Room Status}
    Status -->|Dirty - Checkout| Priority1[HIGH PRIORITY]
    Status -->|Dirty - Stayover| Priority2[MEDIUM PRIORITY]
    Status -->|Dirty| Priority3[NORMAL PRIORITY]
    Status -->|Clean| NoAction[No Action Needed]
    
    Priority1 --> Clean[Clean the Room]
    Priority2 --> Clean
    Priority3 --> Clean
    
    Clean --> Inspect[Inspect Room Quality]
    Inspect --> QC{Quality Check}
    QC -->|Pass| MarkClean[Mark as Clean in System]
    QC -->|Fail| Clean
    
    MarkClean --> Update[Status Updates]
    Update --> Notify[Notify Front Desk]
    Notify --> Available[Room Available for Assignment]
    
    GV3 --> SelectRoom[Select Room to Clean]
    SelectRoom --> Checkbox[Check 'Mark it Clean']
    Checkbox --> MarkClean
    
    style HK fill:#e74c3c
    style HKDash fill:#ec7063
    style Priority1 fill:#c0392b
    style Priority2 fill:#e67e22
    style Priority3 fill:#f39c12
    style MarkClean fill:#2ecc71
```

---

## 5. Reservation Management Flow

```mermaid
graph TB
    ResStart([Reservation Module]) --> ResView[Calendar View]
    
    ResView --> ViewOptions{View Options}
    ViewOptions -->|Day| DayView[Day View]
    ViewOptions -->|Week| WeekView[Week View]
    ViewOptions -->|Month| MonthView[Month View]
    
    ResView --> Actions{User Actions}
    Actions -->|Create| CreateRes[Create New Reservation]
    Actions -->|Click Booking| ViewBooking[View Booking Details]
    Actions -->|Search| SearchRes[Search Reservation]
    Actions -->|Filter| FilterRes[Filter by Room/Status]
    
    CreateRes --> NewBookingForm[New Booking Form]
    NewBookingForm --> NBF1[Guest Information]
    NewBookingForm --> NBF2[Select Dates]
    NewBookingForm --> NBF3[Select Room Type]
    NewBookingForm --> NBF4[Select Rate Plan]
    NewBookingForm --> NBF5[Add Special Requests]
    NewBookingForm --> NBF6[Calculate Total]
    NBF6 --> SaveBooking[Save Booking]
    SaveBooking --> BookingCreated[Booking Created]
    BookingCreated --> SendConfirm[Send Confirmation]
    
    ViewBooking --> BookingDetails[Booking Details Panel]
    BookingDetails --> Tabs{Select Tab}
    Tabs -->|Booking Info| Tab1[Booking Information]
    Tabs -->|Customer Info| Tab2[Customer Information]
    Tabs -->|Notes| Tab3[Notes & Comments]
    
    BookingDetails --> BookingActions{Available Actions}
    BookingActions -->|Check-in| ActionCI[Check-in Process]
    BookingActions -->|Print Card| ActionPrint[Print Registration Card]
    BookingActions -->|View Folio| ActionFolio[View Billing Folio]
    BookingActions -->|Settle Dues| ActionPay[Payment Process]
    BookingActions -->|Magic Link| ActionMagic[Send Magic Link]
    BookingActions -->|Hold| ActionHold[Put on Hold]
    BookingActions -->|Cancel| ActionCancel[Cancel Booking]
    BookingActions -->|Lock| ActionLock[Lock Booking]
    BookingActions -->|Edit| ActionEdit[Edit Reservation]
    BookingActions -->|Modify Dates| ActionDates[Modify Check-in/out]
    BookingActions -->|Assign Room| ActionAssign[Assign Room]
    BookingActions -->|Unassign| ActionUnassign[Unassign Room]
    
    ActionCI --> CheckInFlow[Go to Check-in Flow]
    ActionPay --> PaymentFlow[Go to Payment Flow]
    ActionMagic --> MagicLinkFlow[Go to Magic Link Flow]
    
    ActionCancel --> ConfirmCancel{Confirm Cancellation?}
    ConfirmCancel -->|Yes| CancelPolicy[Apply Cancellation Policy]
    CancelPolicy --> RefundCalc[Calculate Refund]
    RefundCalc --> ProcessCancel[Process Cancellation]
    ProcessCancel --> SendCancelEmail[Send Cancellation Email]
    ConfirmCancel -->|No| BookingDetails
    
    style ResStart fill:#3498db
    style CreateRes fill:#2ecc71
    style ViewBooking fill:#9b59b6
    style ActionCI fill:#e67e22
    style ActionCancel fill:#e74c3c
```

---

## 6. Billing & Payment Flow

```mermaid
graph TB
    BillStart([Billing Module]) --> OpenFolio[Open Guest Folio]
    
    OpenFolio --> FolioView[Folio Summary View]
    FolioView --> FolioSections{Folio Sections}
    
    FolioSections --> Section1[Booking Charges]
    FolioSections --> Section2[Tax Breakdown]
    FolioSections --> Section3[Additional Charges]
    FolioSections --> Section4[Payments Made]
    FolioSections --> Section5[Balance Due]
    
    Section1 --> Charges[Room Charges by Date]
    Section2 --> Taxes[Occupancy, Sales, Municipality Tax]
    Section3 --> AddOns{Additional Items}
    AddOns --> Minibar[Minibar Charges]
    AddOns --> RoomService[Room Service]
    AddOns --> Laundry[Laundry]
    AddOns --> Other[Other Services]
    
    FolioView --> FolioActions{Actions}
    FolioActions -->|Settle Dues| SettleDues[Payment Process]
    FolioActions -->|Add Charge| AddCharge[Add Item to Folio]
    FolioActions -->|Apply Discount| ApplyDiscount[Apply Discount/Coupon]
    FolioActions -->|Print| PrintFolio[Print Folio]
    FolioActions -->|Email| EmailFolio[Email to Guest]
    
    SettleDues --> PaymentMethod{Select Payment Method}
    PaymentMethod -->|Cash| CashPay[Cash Payment]
    PaymentMethod -->|Card Offline| CardOffline[Offline Card Payment]
    PaymentMethod -->|Card Online| CardOnline[Stripe Gateway]
    PaymentMethod -->|UPI| UPIPay[UPI Payment]
    PaymentMethod -->|Bank Transfer| BankTransfer[Bank Transfer]
    PaymentMethod -->|Cheque| ChequePay[Cheque Payment]
    PaymentMethod -->|Saved Card| SavedCard[Use Saved Card]
    PaymentMethod -->|Other| OtherPay[Other Payment Mode]
    
    CashPay --> EnterAmount[Enter Amount]
    CardOffline --> EnterAmount
    UPIPay --> EnterAmount
    BankTransfer --> EnterAmount
    ChequePay --> EnterAmount
    OtherPay --> EnterAmount
    
    CardOnline --> StripeFlow[Process via Stripe]
    StripeFlow --> StripeAuth{Authorization}
    StripeAuth -->|Success| PaymentSuccess
    StripeAuth -->|Failed| PaymentFailed[Payment Failed]
    PaymentFailed --> Retry{Retry Payment?}
    Retry -->|Yes| PaymentMethod
    Retry -->|No| FolioView
    
    SavedCard --> SelectCard[Select Saved Card]
    SelectCard --> ProcessCard[Process Payment]
    ProcessCard --> PaymentSuccess
    
    EnterAmount --> PartialFull{Full or Partial?}
    PartialFull -->|Full Payment| FullPay[Pay Full Balance]
    PartialFull -->|Partial| PartialPay[Pay Partial Amount]
    
    FullPay --> PaymentSuccess[Payment Successful]
    PartialPay --> PaymentSuccess
    
    PaymentSuccess --> UpdateFolio[Update Folio Balance]
    UpdateFolio --> GenerateReceipt[Generate Receipt]
    GenerateReceipt --> ReceiptAction{Receipt Action}
    ReceiptAction -->|Print| PrintReceipt[Print Receipt]
    ReceiptAction -->|Email| EmailReceipt[Email Receipt]
    ReceiptAction -->|Both| BothReceipt[Print & Email]
    
    PrintReceipt --> Complete[Payment Complete]
    EmailReceipt --> Complete
    BothReceipt --> Complete
    
    Complete --> CheckBalance{Check Balance}
    CheckBalance -->|Balance = 0| FullyPaid[Fully Paid]
    CheckBalance -->|Balance > 0| PartiallyPaid[Partially Paid]
    
    ApplyDiscount --> DiscountType{Discount Type}
    DiscountType -->|Percentage| PercentDisc[Enter Percentage]
    DiscountType -->|Fixed Amount| FixedDisc[Enter Amount]
    DiscountType -->|Coupon Code| CouponCode[Enter Coupon]
    
    PercentDisc --> ApplyDisc[Apply to Folio]
    FixedDisc --> ApplyDisc
    CouponCode --> ValidateCoupon{Valid Coupon?}
    ValidateCoupon -->|Yes| ApplyDisc
    ValidateCoupon -->|No| ErrorCoupon[Invalid Coupon]
    ErrorCoupon --> FolioView
    
    ApplyDisc --> RecalculateTotal[Recalculate Total]
    RecalculateTotal --> FolioView
    
    style BillStart fill:#9b59b6
    style PaymentMethod fill:#f39c12
    style PaymentSuccess fill:#2ecc71
    style PaymentFailed fill:#e74c3c
    style Complete fill:#16a085
```

---

## 7. Magic Link Flow

```mermaid
graph TB
    MagicStart([Magic Link Module]) --> OpenBooking[Open Booking Details]
    
    OpenBooking --> ClickMagic[Click 'Send Magic Link']
    ClickMagic --> MagicDialog[Magic Link Dialog]
    
    MagicDialog --> LinkDisplay[Display Magic Link URL]
    LinkDisplay --> AutoFill[Auto-fill Guest Email & Phone]
    
    AutoFill --> EditContact{Edit Contact Info?}
    EditContact -->|Yes| ModifyEmail[Modify Email]
    EditContact -->|Yes| ModifyPhone[Modify Phone]
    EditContact -->|No| SendOptions
    
    ModifyEmail --> SendOptions{Send Via}
    ModifyPhone --> SendOptions
    
    SendOptions -->|Email| SendEmail[Send via Email]
    SendOptions -->|SMS| SendSMS[Send via SMS]
    SendOptions -->|Both| SendBoth[Send via Email & SMS]
    SendOptions -->|Copy Link| CopyLink[Copy Link to Clipboard]
    
    SendEmail --> EmailSent[Email Sent Successfully]
    SendSMS --> SMSSent[SMS Sent Successfully]
    SendBoth --> BothSent[Email & SMS Sent]
    CopyLink --> LinkCopied[Link Copied]
    
    EmailSent --> GuestReceives[Guest Receives Magic Link]
    SMSSent --> GuestReceives
    BothSent --> GuestReceives
    
    GuestReceives --> GuestClicks[Guest Clicks Link]
    GuestClicks --> MagicPortal[Magic Link Portal Opens]
    
    MagicPortal --> PortalHome[Itinerary Home Page]
    PortalHome --> DisplayInfo{Display Information}
    
    DisplayInfo --> PropInfo[Property Information]
    DisplayInfo --> CheckInOut[Check-in/out Details]
    DisplayInfo --> RoomDetails[Room Details]
    DisplayInfo --> PaymentInfo[Payment Information]
    DisplayInfo --> MapDirections[Map & Directions]
    
    PropInfo --> CallProperty[Call Property Button]
    PropInfo --> GetDirections[Get Direction Button]
    
    PortalHome --> GuestActions{Guest Actions}
    GuestActions -->|Self Check-in| SelfCheckin[Self Check-in Flow]
    GuestActions -->|Room Upgrade| RoomUpgrade[View Upgrade Options]
    GuestActions -->|Extend Stay| ExtendStay[Request Extension]
    GuestActions -->|Add Services| AddServices[Purchase Add-ons]
    GuestActions -->|Make Payment| GuestPayment[Online Payment]
    GuestActions -->|Contact| ContactProperty[Contact Property]
    
    SelfCheckin --> VerifyIdentity[Verify Identity]
    VerifyIdentity --> UploadID[Upload ID Document]
    UploadID --> FillDetails[Fill Required Details]
    FillDetails --> ESign[Electronic Signature]
    ESign --> SubmitCheckin[Submit Check-in]
    SubmitCheckin --> CheckinApproval{Approval Status}
    CheckinApproval -->|Approved| CheckinSuccess[Check-in Successful]
    CheckinApproval -->|Pending| CheckinPending[Awaiting Approval]
    CheckinSuccess --> DigitalKey[Receive Digital Room Key]
    
    RoomUpgrade --> ViewUpgrades[View Available Upgrades]
    ViewUpgrades --> SelectUpgrade[Select Upgrade]
    SelectUpgrade --> UpgradePrice[View Price Difference]
    UpgradePrice --> ConfirmUpgrade{Confirm Upgrade?}
    ConfirmUpgrade -->|Yes| ProcessUpgrade[Process Upgrade Payment]
    ConfirmUpgrade -->|No| PortalHome
    ProcessUpgrade --> UpgradeSuccess[Upgrade Confirmed]
    
    ExtendStay --> SelectNewDate[Select New Checkout Date]
    SelectNewDate --> CheckAvailability[Check Availability]
    CheckAvailability --> Available{Room Available?}
    Available -->|Yes| ShowExtendPrice[Show Additional Cost]
    Available -->|No| NotAvailable[Not Available - Contact Front Desk]
    ShowExtendPrice --> ConfirmExtend{Confirm Extension?}
    ConfirmExtend -->|Yes| ProcessExtension[Process Extension]
    ConfirmExtend -->|No| PortalHome
    ProcessExtension --> ExtendSuccess[Stay Extended]
    
    AddServices --> ServiceCatalog[View Service Catalog]
    ServiceCatalog --> SelectService[Select Services]
    SelectService --> AddToCart[Add to Cart]
    AddToCart --> ReviewCart[Review Cart]
    ReviewCart --> CheckoutServices[Checkout]
    CheckoutServices --> ServicePayment[Process Payment]
    ServicePayment --> ServiceSuccess[Services Booked]
    
    GuestPayment --> ViewBalance[View Outstanding Balance]
    ViewBalance --> PaymentGateway[Online Payment Gateway]
    PaymentGateway --> ProcessGuestPay[Process Payment]
    ProcessGuestPay --> PaySuccess{Payment Status}
    PaySuccess -->|Success| GuestPaymentSuccess[Payment Successful]
    PaySuccess -->|Failed| GuestPaymentFailed[Payment Failed - Retry]
    GuestPaymentSuccess --> UpdateBalance[Balance Updated]
    
    style MagicStart fill:#1abc9c
    style MagicPortal fill:#16a085
    style GuestActions fill:#f39c12
    style CheckinSuccess fill:#2ecc71
    style DigitalKey fill:#3498db
```

---

## 8. Housekeeping Operations Flow

```mermaid
graph TB
    HKStart([Housekeeping Operations]) --> HKLogin[Housekeeping Staff Login]
    
    HKLogin --> HKDashboard[Housekeeping Dashboard]
    HKDashboard --> StatusOverview[Room Status Overview]
    
    StatusOverview --> Stats{Status Statistics}
    Stats --> Clean[Clean: 0]
    Stats --> CleanOccupied[Clean Occupied: 0]
    Stats --> Dirty[Dirty: 2]
    Stats --> DirtyStayover[Dirty Stayover: 13]
    Stats --> DirtyCheckout[Dirty Checkout: 55]
    Stats --> OutOfOrder[Out of Order: 0]
    Stats --> TotalClean[Total Clean: 0]
    Stats --> TotalDirty[Total Dirty: 70]
    Stats --> AllRooms[All Rooms: 70]
    
    HKDashboard --> ViewToggle{Select View}
    ViewToggle -->|List View| ListView[List View - Table Format]
    ViewToggle -->|Grid View| GridView[Grid View - Card Format]
    
    ListView --> ListFeatures{List View Features}
    ListFeatures --> Search[Search Rooms]
    ListFeatures --> FilterStatus[Filter by Status]
    ListFeatures --> FilterRoom[Filter by Room Type]
    ListFeatures --> FilterStaff[Filter by Staff]
    ListFeatures --> Pagination[Pagination Controls]
    ListFeatures --> Export[Export Report]
    
    ListView --> RoomList[Display Room List]
    RoomList --> RoomColumns{Column Information}
    RoomColumns --> Col1[Room ID]
    RoomColumns --> Col2[Room Type]
    RoomColumns --> Col3[Status]
    RoomColumns --> Col4[Staff Name]
    RoomColumns --> Col5[Staff Email]
    RoomColumns --> Col6[Staff Remark]
    RoomColumns --> Col7[Supervisor]
    
    RoomList --> SelectFromList[Select Room from List]
    SelectFromList --> ViewRoomDetail[View Room Details]
    
    GridView --> GridFeatures{Grid View Features}
    GridFeatures --> SelectStaff[Select Staff Dropdown]
    GridFeatures --> SelectRoomType[Select Room Type]
    GridFeatures --> GridInfo[Info: Admin Only Access]
    
    GridView --> RoomCards[Display Room Cards]
    RoomCards --> CardInfo{Card Information}
    CardInfo --> RoomNumber[Room Number]
    CardInfo --> StatusIndicator[Status Indicator - Red/Green]
    CardInfo --> CheckBox[Mark it Clean Checkbox]
    
    StatusIndicator --> RedDot[🔴 Red = Dirty]
    StatusIndicator --> GreenDot[🟢 Green = Clean]
    
    RoomCards --> SelectFromGrid[Select Room Card]
    
    SelectFromList --> StartCleaning[Start Cleaning Process]
    SelectFromGrid --> StartCleaning
    
    StartCleaning --> AssignToSelf{Assigned to Me?}
    AssignToSelf -->|No| RequestAssign[Request Assignment]
    AssignToSelf -->|Yes| BeginClean[Begin Cleaning]
    
    RequestAssign --> AdminApprove{Admin Approval}
    AdminApprove -->|Approved| BeginClean
    AdminApprove -->|Denied| HKDashboard
    
    BeginClean --> CleaningTasks{Cleaning Tasks}
    CleaningTasks --> Task1[Change Bed Linens]
    CleaningTasks --> Task2[Clean Bathroom]
    CleaningTasks --> Task3[Vacuum/Mop Floor]
    CleaningTasks --> Task4[Dust Surfaces]
    CleaningTasks --> Task5[Restock Amenities]
    CleaningTasks --> Task6[Empty Trash]
    CleaningTasks --> Task7[Check Minibar]
    CleaningTasks --> Task8[Arrange Furniture]
    
    Task1 --> TaskComplete1[Complete]
    Task2 --> TaskComplete2[Complete]
    Task3 --> TaskComplete3[Complete]
    Task4 --> TaskComplete4[Complete]
    Task5 --> TaskComplete5[Complete]
    Task6 --> TaskComplete6[Complete]
    Task7 --> TaskComplete7[Complete]
    Task8 --> TaskComplete8[Complete]
    
    TaskComplete1 --> AllTasksDone{All Tasks Complete?}
    TaskComplete2 --> AllTasksDone
    TaskComplete3 --> AllTasksDone
    TaskComplete4 --> AllTasksDone
    TaskComplete5 --> AllTasksDone
    TaskComplete6 --> AllTasksDone
    TaskComplete7 --> AllTasksDone
    TaskComplete8 --> AllTasksDone
    
    AllTasksDone -->|Yes| QualityCheck[Quality Check]
    AllTasksDone -->|No| CleaningTasks
    
    QualityCheck --> Inspection{Inspection Result}
    Inspection -->|Pass| MarkCleanSystem[Mark as Clean in System]
    Inspection -->|Fail| IssueFound{Issue Type}
    
    IssueFound -->|Minor| FixIssue[Fix Issue]
    IssueFound -->|Major| ReportIssue[Report to Supervisor]
    
    FixIssue --> QualityCheck
    ReportIssue --> SupervisorCheck{Supervisor Decision}
    SupervisorCheck -->|Re-clean| BeginClean
    SupervisorCheck -->|Mark Out of Order| MarkOOO[Mark as Out of Order]
    SupervisorCheck -->|Fix & Continue| FixIssue
    
    MarkCleanSystem --> SystemUpdate[System Updates Status]
    SystemUpdate --> NotifyFrontDesk[Notify Front Desk]
    NotifyFrontDesk --> RoomAvailable[Room Available for Assignment]
    
    RoomAvailable --> Stats2{Update Statistics}
    Stats2 --> DecreaseDirty[Dirty Count -1]
    Stats2 --> IncreaseClean[Clean Count +1]
    
    DecreaseDirty --> RefreshDashboard[Refresh Dashboard]
    IncreaseClean --> RefreshDashboard
    
    RefreshDashboard --> NextRoom{More Rooms to Clean?}
    NextRoom -->|Yes| HKDashboard
    NextRoom -->|No| ShiftComplete[Shift Complete]
    
    ShiftComplete --> GenerateReport[Generate Shift Report]
    GenerateReport --> SubmitReport[Submit to Supervisor]
    SubmitReport --> Logout[Logout]
    
    style HKStart fill:#e74c3c
    style BeginClean fill:#f39c12
    style MarkCleanSystem fill:#2ecc71
    style RoomAvailable fill:#3498db
    style ShiftComplete fill:#16a085
```

---

## 9. Guest Check-in Journey

```mermaid
graph TB
    CheckInStart([Guest Arrives]) --> Reception[Approach Front Desk]
    
    Reception --> FDGreet[Front Desk Greets Guest]
    FDGreet --> AskBooking[Ask for Booking Information]
    
    AskBooking --> GuestProvides{Guest Provides}
    GuestProvides -->|Name| SearchName[Search by Name]
    GuestProvides -->|Booking ID| SearchID[Search by Booking ID]
    GuestProvides -->|Phone| SearchPhone[Search by Phone]
    GuestProvides -->|Email| SearchEmail[Search by Email]
    
    SearchName --> FindBooking{Booking Found?}
    SearchID --> FindBooking
    SearchPhone --> FindBooking
    SearchEmail --> FindBooking
    
    FindBooking -->|No| NoBooking[No Booking Found]
    FindBooking -->|Yes| OpenBooking[Open Booking Details]
    
    NoBooking --> CreateWalkIn{Create Walk-in?}
    CreateWalkIn -->|Yes| CreateBooking[Create New Booking]
    CreateWalkIn -->|No| ApologizeGuest[Apologize - Cannot Check-in]
    
    CreateBooking --> NewBookingProcess[New Booking Process]
    NewBookingProcess --> OpenBooking
    
    OpenBooking --> VerifyDetails[Verify Booking Details]
    VerifyDetails --> CheckDetails{Verify Information}
    CheckDetails --> GuestName[Guest Name]
    CheckDetails --> RoomType[Room Type]
    CheckDetails --> CheckInDate[Check-in Date]
    CheckDetails --> CheckOutDate[Check-out Date]
    CheckDetails --> NumGuests[Number of Guests]
    CheckDetails --> SpecialRequests[Special Requests]
    
    VerifyDetails --> DetailsCorrect{Details Correct?}
    DetailsCorrect -->|No| ModifyDetails[Modify Booking Details]
    DetailsCorrect -->|Yes| RequestID[Request Guest ID]
    
    ModifyDetails --> SaveChanges[Save Changes]
    SaveChanges --> RequestID
    
    RequestID --> VerifyID[Verify Guest Identity]
    VerifyID --> IDTypes{ID Document Type}
    IDTypes --> Passport[Passport]
    IDTypes --> DrivingLicense[Driving License]
    IDTypes --> NationalID[National ID]
    IDTypes --> Other[Other Government ID]
    
    Passport --> ScanID[Scan/Copy ID Document]
    DrivingLicense --> ScanID
    NationalID --> ScanID
    Other --> ScanID
    
    ScanID --> AttachToBooking[Attach to Booking]
    AttachToBooking --> RoomAssignment{Room Assigned?}
    
    RoomAssignment -->|No| CheckAvail[Check Room Availability]
    RoomAssignment -->|Yes| RoomReady
    
    CheckAvail --> AvailRooms{Available Rooms?}
    AvailRooms -->|No| NoRooms[No Rooms Available]
    AvailRooms -->|Yes| SelectRoom[Select Room]
    
    NoRooms --> OfferAlternative{Offer Alternative?}
    OfferAlternative -->|Upgrade| OfferUpgrade[Offer Upgrade]
    OfferAlternative -->|Wait| WaitForRoom[Wait for Room]
    OfferAlternative -->|Cancel| CancelCheckin[Cancel Check-in]
    
    OfferUpgrade --> GuestAccepts{Guest Accepts?}
    GuestAccepts -->|Yes| AdjustPrice[Adjust Price]
    GuestAccepts -->|No| WaitForRoom
    
    AdjustPrice --> SelectRoom
    SelectRoom --> AssignRoom[Assign Room to Booking]
    AssignRoom --> RoomReady{Room Ready?}
    
    RoomReady -->|Not Clean| WaitCleaning[Wait for Housekeeping]
    RoomReady -->|Clean| ProceedPayment[Proceed to Payment]
    
    WaitCleaning --> CheckStatus{Check Room Status}
    CheckStatus -->|Still Dirty| ContactHK[Contact Housekeeping]
    CheckStatus -->|Now Clean| ProceedPayment
    
    ContactHK --> UrgentClean[Request Urgent Cleaning]
    UrgentClean --> WaitCleaning
    
    ProceedPayment --> ReviewCharges[Review Charges with Guest]
    ReviewCharges --> ShowFolio[Show Folio Summary]
    ShowFolio --> FolioBreakdown{Folio Items}
    FolioBreakdown --> RoomCharges[Room Charges]
    FolioBreakdown --> TaxCharges[Tax Breakdown]
    FolioBreakdown --> TotalAmount[Total Amount]
    
    ShowFolio --> PaymentPolicy{Payment Policy}
    PaymentPolicy -->|Full Payment| RequireFullPay[Require Full Payment]
    PaymentPolicy -->|Deposit| RequireDeposit[Require Deposit]
    PaymentPolicy -->|Pay at Checkout| NoPaymentNow[No Payment Required Now]
    
    RequireFullPay --> CollectPayment[Collect Payment]
    RequireDeposit --> CollectPayment
    NoPaymentNow --> CaptureCard[Capture Card Details]
    
    CollectPayment --> PaymentMethodCI{Payment Method}
    PaymentMethodCI --> ProcessPaymentCI[Process Payment]
    ProcessPaymentCI --> PaymentSuccessCI{Payment Success?}
    PaymentSuccessCI -->|Yes| PaymentComplete[Payment Recorded]
    PaymentSuccessCI -->|No| PaymentFailed[Payment Failed]
    PaymentFailed --> RetryPayment{Retry?}
    RetryPayment -->|Yes| CollectPayment
    RetryPayment -->|No| CancelCheckin
    
    CaptureCard --> SaveCardInfo[Save Card Information]
    SaveCardInfo --> PaymentComplete
    PaymentComplete --> PrintRegCard[Print Registration Card]
    
    PrintRegCard --> GuestSign[Guest Signs Reg Card]
    GuestSign --> ScanSignature[Scan Signed Document]
    ScanSignature --> AttachSignature[Attach to Booking]
    
    AttachSignature --> AdditionalServices{Offer Additional Services?}
    AdditionalServices -->|Breakfast| OfferBreakfast[Offer Breakfast Package]
    AdditionalServices -->|Parking| OfferParking[Offer Parking]
    AdditionalServices -->|Spa| OfferSpa[Offer Spa Services]
    AdditionalServices -->|None| PrepareKey
    
    OfferBreakfast --> GuestInterested{Guest Interested?}
    OfferParking --> GuestInterested
    OfferSpa --> GuestInterested
    GuestInterested -->|Yes| AddService[Add to Folio]
    GuestInterested -->|No| PrepareKey
    AddService --> PrepareKey[Prepare Room Key]
    
    PrepareKey --> KeyType{Key Type}
    KeyType -->|Card Key| ProgramCardKey[Program Card Key]
    KeyType -->|Digital Key| SendDigitalKey[Send Digital Key to App]
    KeyType -->|Physical Key| ProvidePhysicalKey[Provide Physical Key]
    
    ProgramCardKey --> KeyReady[Key Ready]
    SendDigitalKey --> KeyReady
    ProvidePhysicalKey --> KeyReady
    
    KeyReady --> PropertyOrientation[Provide Property Information]
    PropertyOrientation --> Inform{Inform Guest About}
    Inform --> WiFiInfo[WiFi Password]
    Inform --> BreakfastTime[Breakfast Timings]
    Inform --> CheckoutTime[Checkout Time]
    Inform --> Amenities[Property Amenities]
    Inform --> EmergencyInfo[Emergency Procedures]
    
    PropertyOrientation --> OfferAssistance[Offer Luggage Assistance]
    OfferAssistance --> AssistanceNeeded{Assistance Needed?}
    AssistanceNeeded -->|Yes| CallPorter[Call Porter]
    AssistanceNeeded -->|No| DirectToRoom
    
    CallPorter --> DirectToRoom[Direct Guest to Room]
    DirectToRoom --> MarkCheckedIn[Mark as Checked In - System]
    
    MarkCheckedIn --> UpdateStatus[Update Booking Status]
    UpdateStatus --> NotifyHK[Notify Housekeeping - Room Occupied]
    NotifyHK --> SendConfirmation[Send Check-in Confirmation Email]
    
    SendConfirmation --> OfferMagicLink{Send Magic Link?}
    OfferMagicLink -->|Yes| SendMagic[Send Magic Link]
    OfferMagicLink -->|No| CheckInComplete
    
    SendMagic --> CheckInComplete[✓ Check-in Complete]
    CheckInComplete --> WishGoodStay[Wish Guest Pleasant Stay]
    
    style CheckInStart fill:#3498db
    style VerifyID fill:#f39c12
    style CollectPayment fill:#9b59b6
    style MarkCheckedIn fill:#2ecc71
    style CheckInComplete fill:#16a085
```

---

## 10. Guest Check-out Journey

```mermaid
graph TB
    CheckOutStart([Guest Ready to Checkout]) --> ApproachDesk[Guest Approaches Front Desk]
    
    ApproachDesk --> FDCheckout[Front Desk Receives Guest]
    FDCheckout --> RequestRoom[Request Room Number]
    
    RequestRoom --> SearchGuest[Search Guest Booking]
    SearchGuest --> FindGuest{Booking Found?}
    FindGuest -->|No| NotFound[Booking Not Found]
    FindGuest -->|Yes| OpenGuestFolio[Open Guest Folio]
    
    NotFound --> AskDetails[Ask for More Details]
    AskDetails --> SearchAgain[Search Again]
    SearchAgain --> FindGuest
    
    OpenGuestFolio --> CurrentStatus{Current Status}
    CurrentStatus -->|Not Checked In| ErrorNotCheckedIn[Error: Not Checked In]
    CurrentStatus -->|Already Checked Out| ErrorAlreadyOut[Error: Already Checked Out]
    CurrentStatus -->|Checked In| ProceedCheckout[Proceed with Checkout]
    
    ProceedCheckout --> InquireStay[Inquire About Stay Quality]
    InquireStay --> GuestFeedback{Guest Feedback}
    GuestFeedback -->|Positive| ThankGuest[Thank Guest]
    GuestFeedback -->|Negative| RecordComplaint[Record Complaint]
    GuestFeedback -->|Neutral| Acknowledge[Acknowledge]
    
    RecordComplaint --> EscalateIssue{Escalate?}
    EscalateIssue -->|Yes| NotifyManager[Notify Manager]
    EscalateIssue -->|No| ProceedWithBill
    NotifyManager --> ManagerResponse{Manager Action}
    ManagerResponse --> ApplyComp[Apply Compensation]
    ManagerResponse --> ProceedWithBill[Proceed with Bill]
    
    ThankGuest --> ProceedWithBill
    Acknowledge --> ProceedWithBill
    ApplyComp --> ProceedWithBill
    
    ProceedWithBill --> RoomInspection[Inquire About Room Condition]
    RoomInspection --> CheckMinibar{Check Minibar}
    CheckMinibar --> MinibarUsed{Items Used?}
    MinibarUsed -->|Yes| AddMinibarCharges[Add Minibar Charges to Folio]
    MinibarUsed -->|No| CheckDamage
    
    AddMinibarCharges --> CheckDamage{Check for Damages}
    CheckDamage -->|Damage Found| AssessDamage[Assess Damage]
    CheckDamage -->|No Damage| ReviewFolio
    
    AssessDamage --> CalculateDamage[Calculate Damage Cost]
    CalculateDamage --> InformGuest[Inform Guest of Charge]
    InformGuest --> GuestAgree{Guest Agrees?}
    GuestAgree -->|Yes| AddDamageCharge[Add Damage Charge to Folio]
    GuestAgree -->|No| DisputeProcess[Initiate Dispute Process]
    
    DisputeProcess --> DocumentEvidence[Document Evidence]
    DocumentEvidence --> ManagerDecision[Manager Decision]
    ManagerDecision --> FinalCharge{Final Decision}
    FinalCharge -->|Charge| AddDamageCharge
    FinalCharge -->|Waive| ReviewFolio
    
    AddDamageCharge --> ReviewFolio[Review Complete Folio]
    ReviewFolio --> DisplayFolio[Display Folio to Guest]
    
    DisplayFolio --> FolioSections{Folio Sections}
    FolioSections --> AccomCharges[Accommodation Charges]
    FolioSections --> TaxBreakdown[Tax Breakdown]
    FolioSections --> AddCharges[Additional Charges]
    FolioSections --> PrevPayments[Previous Payments]
    FolioSections --> CurrentBalance[Current Balance]
    
    DisplayFolio --> GuestReview{Guest Reviews Folio}
    GuestReview -->|Dispute| HandleDispute[Handle Dispute]
    GuestReview -->|Approve| CheckBalance
    
    HandleDispute --> ResolveDispute[Resolve with Guest]
    ResolveDispute --> AdjustFolio[Adjust Folio if Needed]
    AdjustFolio --> CheckBalance{Check Balance}
    
    CheckBalance -->|Balance = 0| AlreadyPaid[Already Fully Paid]
    CheckBalance -->|Balance > 0| ProcessPayment[Process Final Payment]
    CheckBalance -->|Balance < 0| RefundDue[Refund Due to Guest]
    
    AlreadyPaid --> PrepareReceipt[Prepare Receipt]
    
    ProcessPayment --> SelectPaymentMethod{Payment Method}
    SelectPaymentMethod -->|Same as Check-in| UseExistingMethod[Use Existing Payment Method]
    SelectPaymentMethod -->|New Method| NewPaymentMethod[Select New Payment Method]
    
    UseExistingMethod --> ChargeCard[Charge Saved Card]
    NewPaymentMethod --> ProcessNewPayment[Process New Payment]
    
    ChargeCard --> PaymentResult{Payment Result}
    ProcessNewPayment --> PaymentResult
    PaymentResult -->|Success| PaymentCompleted[Payment Completed]
    PaymentResult -->|Failed| PaymentError[Payment Error]
    
    PaymentError --> RetryCheckout{Retry Payment?}
    RetryCheckout -->|Yes| ProcessPayment
    RetryCheckout -->|No| HoldCheckout[Hold Checkout - Unresolved]
    
    PaymentCompleted --> UpdateFolioFinal[Update Final Folio]
    UpdateFolioFinal --> PrepareReceipt
    
    RefundDue --> CalculateRefund[Calculate Refund Amount]
    CalculateRefund --> RefundMethod{Refund Method}
    RefundMethod -->|Original Payment| RefundOriginal[Refund to Original Method]
    RefundMethod -->|Cash| RefundCash[Refund Cash]
    RefundMethod -->|Bank Transfer| RefundBank[Refund via Bank]
    
    RefundOriginal --> ProcessRefund[Process Refund]
    RefundCash --> ProcessRefund
    RefundBank --> ProcessRefund
    ProcessRefund --> RefundComplete[Refund Processed]
    RefundComplete --> PrepareReceipt
    
    PrepareReceipt --> GenerateReceipt[Generate Final Receipt]
    GenerateReceipt --> ReceiptOptions{Receipt Options}
    ReceiptOptions -->|Print| PrintReceiptCO[Print Receipt]
    ReceiptOptions -->|Email| EmailReceiptCO[Email Receipt]
    ReceiptOptions -->|Both| BothReceiptCO[Print & Email]
    
    PrintReceiptCO --> ProvideReceipt[Provide Receipt to Guest]
    EmailReceiptCO --> ProvideReceipt
    BothReceiptCO --> ProvideReceipt
    
    ProvideReceipt --> CollectKey[Collect Room Key]
    CollectKey --> KeyReturned{Key Returned?}
    KeyReturned -->|Yes| KeyReceived[Key Received]
    KeyReturned -->|No| MissingKey[Note Missing Key]
    
    MissingKey --> KeyFee{Charge Key Fee?}
    KeyFee -->|Yes| ChargeKeyFee[Charge Key Replacement Fee]
    KeyFee -->|No| WaiveKeyFee[Waive Fee]
    ChargeKeyFee --> KeyReceived
    WaiveKeyFee --> KeyReceived
    
    KeyReceived --> FeedbackRequest[Request Review/Feedback]
    FeedbackRequest --> OfferServices{Offer Future Services}
    OfferServices --> LoyaltyProgram[Mention Loyalty Program]
    OfferServices --> FutureDiscount[Offer Return Discount]
    OfferServices --> Newsletter[Invite Newsletter Signup]
    
    LoyaltyProgram --> SystemCheckout[Mark as Checked Out - System]
    FutureDiscount --> SystemCheckout
    Newsletter --> SystemCheckout
    
    SystemCheckout --> UpdateBookingStatus[Update Booking Status: Checked Out]
    UpdateBookingStatus --> UpdateRoomStatus[Update Room Status: Dirty - Checkout]
    UpdateRoomStatus --> NotifyHousekeeping[Notify Housekeeping]
    NotifyHousekeeping --> ReleaseRoom[Release Room from Guest]
    
    ReleaseRoom --> SendSurvey{Send Guest Survey?}
    SendSurvey -->|Yes| EmailSurvey[Email Satisfaction Survey]
    SendSurvey -->|No| FarewellGuest
    
    EmailSurvey --> FarewellGuest[Thank Guest & Wish Safe Journey]
    FarewellGuest --> PorterAssist{Luggage Assistance?}
    PorterAssist -->|Yes| CallPorterCO[Call Porter]
    PorterAssist -->|No| CheckOutComplete
    
    CallPorterCO --> CheckOutComplete[✓ Checkout Complete]
    CheckOutComplete --> UpdateStats[Update Dashboard Statistics]
    UpdateStats --> ArchiveBooking[Archive Completed Booking]
    
    style CheckOutStart fill:#e67e22
    style ReviewFolio fill:#9b59b6
    style ProcessPayment fill:#f39c12
    style PaymentCompleted fill:#2ecc71
    style CheckOutComplete fill:#16a085
```

---

## 🎨 Legend & Color Coding

### User Roles
- 🟢 **Green (#2ecc71)** = Admin
- 🔵 **Blue (#3498db)** = Front Desk
- 🔴 **Red (#e74c3c)** = Housekeeping

### Status Colors
- 🟢 **Green** = Completed/Success/Clean
- 🔴 **Red** = Dirty/Failed/Error
- 🟡 **Yellow (#f39c12)** = In Progress/Pending
- 🟣 **Purple (#9b59b6)** = Billing/Payment
- 🔵 **Teal (#1abc9c)** = Magic Link/Guest Portal
- 🟠 **Orange (#e67e22)** = Check-in/Check-out

### Decision Points
- 🔶 **Diamond Shape** = Decision Point (Yes/No)
- 🔷 **Hexagon** = Multiple Choice Selection
- 📦 **Rectangle** = Process/Action
- 🎯 **Rounded Rectangle** = Start/End Point

---

## 📱 Integration Points

### External Systems
```mermaid
graph LR
    PMS[PMS System] --> BookingCom[Booking.com API]
    PMS --> Airbnb[Airbnb API]
    PMS --> Stripe[Stripe Payment Gateway]
    PMS --> Email[Email Service SMTP]
    PMS --> SMS[SMS Gateway]
    PMS --> Maps[Google Maps API]
    
    style PMS fill:#3498db
    style BookingCom fill:#003580
    style Airbnb fill:#FF5A5F
    style Stripe fill:#635BFF
```

---

## 🔐 Security & Access Control Flow

```mermaid
graph TB
    Login[User Login] --> ValidateCredentials{Validate Credentials}
    ValidateCredentials -->|Invalid| LoginFail[Login Failed]
    ValidateCredentials -->|Valid| CheckRole{Check User Role}
    
    CheckRole -->|Admin| AdminPermissions[Grant All Permissions]
    CheckRole -->|Front Desk| FDPermissions[Grant Limited Permissions]
    CheckRole -->|Housekeeping| HKPermissions[Grant Restricted Permissions]
    
    AdminPermissions --> AccessMatrix[Access Control Matrix]
    FDPermissions --> AccessMatrix
    HKPermissions --> AccessMatrix
    
    AccessMatrix --> SessionCreate[Create User Session]
    SessionCreate --> TokenGenerate[Generate Session Token]
    TokenGenerate --> Dashboard[Redirect to Dashboard]
    
    Dashboard --> UserAction{User Performs Action}
    UserAction --> CheckPermission{Check Permission}
    CheckPermission -->|Allowed| ExecuteAction[Execute Action]
    CheckPermission -->|Denied| AccessDenied[Access Denied Error]
    
    ExecuteAction --> LogAction[Log Action to Audit Trail]
    LogAction --> UpdateDB[Update Database]
    
    AccessDenied --> ShowError[Show Error Message]
    ShowError --> Dashboard
    
    LoginFail --> IncrementAttempt[Increment Login Attempts]
    IncrementAttempt --> CheckAttempts{Attempts > 5?}
    CheckAttempts -->|Yes| LockAccount[Lock Account]
    CheckAttempts -->|No| Login
    
    LockAccount --> NotifyAdmin[Notify Admin]
    
    style CheckRole fill:#f39c12
    style AccessMatrix fill:#9b59b6
    style ExecuteAction fill:#2ecc71
    style AccessDenied fill:#e74c3c
```

---

## 📊 Data Flow Architecture

```mermaid
graph TB
    Frontend[Frontend - Web/Mobile App] --> API[REST API Gateway]
    API --> Auth[Authentication Service]
    API --> Booking[Booking Service]
    API --> Payment[Payment Service]
    API --> Housekeeping[Housekeeping Service]
    API --> Communication[Communication Service]
    
    Auth --> UserDB[(User Database)]
    Booking --> BookingDB[(Booking Database)]
    Payment --> PaymentDB[(Payment Database)]
    Housekeeping --> HousekeepingDB[(Housekeeping Database)]
    Communication --> MessageDB[(Message Database)]
    
    Payment --> StripeAPI[Stripe API]
    Communication --> EmailAPI[Email Service]
    Communication --> SMSAPI[SMS Service]
    
    Booking --> ChannelManager[Channel Manager]
    ChannelManager --> OTA1[Booking.com]
    ChannelManager --> OTA2[Airbnb]
    ChannelManager --> OTA3[Expedia]
    
    BookingDB --> Analytics[Analytics Engine]
    PaymentDB --> Analytics
    HousekeepingDB --> Analytics
    
    Analytics --> Reports[Reporting Dashboard]
    
    style Frontend fill:#3498db
    style API fill:#2ecc71
    style Analytics fill:#9b59b6
```

---

## 📈 Success Metrics Dashboard

```mermaid
graph TB
    Metrics[PMS Metrics Dashboard] --> Operational[Operational Metrics]
    Metrics --> Financial[Financial Metrics]
    Metrics --> Guest[Guest Metrics]
    Metrics --> Staff[Staff Metrics]
    
    Operational --> AvgCheckIn[Avg Check-in Time]
    Operational --> RoomTurnover[Room Turnover Time]
    Operational --> Occupancy[Occupancy Rate]
    Operational --> SystemUptime[System Uptime]
    
    Financial --> Revenue[Total Revenue]
    Financial --> ADR[Average Daily Rate]
    Financial --> RevPAR[Revenue per Available Room]
    Financial --> PaymentSuccess[Payment Success Rate]
    
    Guest --> Satisfaction[Guest Satisfaction Score]
    Guest --> Repeat[Repeat Guest Rate]
    Guest --> Reviews[Review Ratings]
    Guest --> Complaints[Complaint Resolution Time]
    
    Staff --> Efficiency[Staff Efficiency]
    Staff --> CleaningTime[Avg Cleaning Time]
    Staff --> ErrorRate[Error Rate]
    Staff --> Productivity[Productivity Score]
    
    style Metrics fill:#3498db
    style Operational fill:#2ecc71
    style Financial fill:#9b59b6
    style Guest fill:#e67e22
    style Staff fill:#1abc9c
```

---