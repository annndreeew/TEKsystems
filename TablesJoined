Select *
INTO dws.mv_SurveyData2016
FROM
(Select 'DWS' AS surveyFamily
		, 'Parent' AS surveyTitle
		, '2016' AS surveyYear
		, '0' AS surveyVersion
		, Coalesce(s.[ID #], 'Unknown') AS surveyid
		, Coalesce(s.[Date Started], 'Unknown') AS surveyDate
		, Coalesce(s.[Student School Site Code], 'Unknown') AS schoolid
		, Coalesce(s.[Student School Name], 'Unknown') AS schoolName
		, Coalesce(s.[Submitter IP Address], 'Unknown') AS IP
		, Coalesce(s.[Student ID Number], 'Unknown') AS studentid
		, Coalesce(s.[Student Birth Date], 'Unknown') AS bdate
		, Coalesce(s.[Response Language], 'Unknown') AS surveyLanguage
		, 'Unknown' AS Parent
		, Coalesce(stu.[StudentGradeLevelCode], 'Unknown') AS gradeLevel
		, Coalesce(s.[Time Started], 'Unknown') AS starttime
		, Coalesce(s.[Time Submitted], 'Unknown') AS endtime  
		, datediff(ss,s.[Time Started],s.[Time Submitted])/60.0 AS minutesToComplete
		, Coalesce(s.[ResponseNumber], 'No response') AS responses
		, Coalesce(s.[QuestionNumber], 'Unknown') AS questions
		, Coalesce(stu.[StudentGenderDescription], 'Unknown') AS StudentGenderDescription
		, Coalesce(stu.[StudentEthnicityDescription], 'Unknown') AS StudentEthnicityDescription
		, Coalesce(stu.[IEPIndicator], 'Unknown') AS IEPIndicator
		, Coalesce(stu.[LEPIndicator], 'Unknown') AS LEPIndicator
		, Coalesce(stu.[Section504Indicator], 'Unknown') AS section504indicator
		, Coalesce(ed.[EducationOrganizationShortName], 'Unknown') AS EducationOrganizationShortName
		, Coalesce(ed.[SchoolCategoryDescription], 'Unknown') AS SchoolCategoryDescription
		, Coalesce(ed.[AcademicOrganizationalUnitDescription], 'Unknown') AS AcademicOrganizationUnitDescription
		, Coalesce(ed.[TrusteeDistrict], 'Unknown') AS TrusteeDistrict
		, Coalesce(ed.[TitleIIndicator], 'Unknown') AS TitleIIndicator
		, Coalesce(ed.[EducationOrganizationMagnetIndicator], 'Unknown') AS EducationOrganizationMagnetIndicator
		, Coalesce(ed.[YearRoundIndicator], 'Unknown') AS YearRoundIndicator
		, Case 
			when s.QuestionNumber IN (Select Distinct ItemNumber
					From dws.LongTextResponseStudent2016_backup r
					Where r.ResponseNumber = '3' AND r.ResponseText = '' ) AND s.ResponseNumber IN('4','5') 
				then CAST((s.[ResponseNumber] - 1) AS nvarchar)
			else s.[ResponseNumber] 
			end as responseIndicator
		, Coalesce(s.[QuestionNumber], 'Unknown') AS ItemNumber
		, Coalesce(r.[ItemText], 'No response') AS ItemText
		, Coalesce(s.[ResponseNumber], 'No response') AS responseValue
		, Coalesce(r.[ResponseText], 'No response') AS responseLabel
		, rq.[Student] AS Stu
	    , rq.[Parent] AS Par
	    , rq.[Staff] AS Staff
		, Coalesce(rq.[Category], 'Unknown') AS Category
		, Coalesce(rq.[questiontext], 'No response') AS questiontext
From dws.LongparentSurvey2016_backup s
LEFT JOIN dws.LongTextResponseParent2016_backup r 
ON s.QuestionNumber=r.ItemNumber AND s.ResponseNumber=r.ResponseNumber
LEFT JOIN sdm.dbo.DimStudent stu
ON stu.[StudentNumber]=s.[Student ID Number] AND s.[Date Submitted] >= stu.[StudentRowEffectiveDate]
AND s.[Date Submitted] <= Stu.[StudentRowExpirationDate]
LEFT JOIN sdm.curr.DimEducationOrganization ed
ON ed.[EducationOrganizationID] = s.[Student School Site Code]
LEFT JOIN dws.RelatedQuestions2016 rq
ON rq.[Parent] = s.[QuestionNumber] 
UNION
SELECT 'DWS' AS SurveyFamily
	   , 'Student' AS SurveyTitle
	   , '2016' AS SurveyYear
	   , '0' AS SurveyVersion
	   , Coalesce(s.[ID #], 'Unknown') AS surveyid
	   , Coalesce(s.[Date Started], 'Unknown') AS SurveyDate
	   , Coalesce(s.[Student School Site Code], 'Unknown') AS Schoolid
	   , Coalesce(s.[Student School Name], 'Unknown') AS SchoolName
	   , Coalesce(s.[Submitter IP Address], 'Unknown') AS IP
	   , Coalesce(s.[Student ID Number], 'Unknown') AS Studentid
	   , Coalesce(s.[Student Birth Date], 'Unknown') AS bdate
	   , Coalesce(s.[Response Language], 'Unknown') AS SurveyLanguage
	   , 'Unknown' AS Parent
	   , Coalesce(stu.[StudentGradeLevelCode], 'Unknown') AS gradeLevel
	   , Coalesce(s.[Time Started], 'Unknown') AS starttime
	   , Coalesce(s.[Time Submitted], 'Unknown') AS endtime 
	   , datediff(ss,s.[Time Started],s.[Time Submitted])/60.0 AS [minutesToComplete]
	   , Coalesce(s.[ResponseNumber], 'No response') AS responses
	   , Coalesce(s.[QuestionNumber], 'Unknown') AS questions
	   , Coalesce(stu.[StudentGenderDescription], 'Unknown') AS StudentGenderDescription
	   , Coalesce(stu.[StudentEthnicityDescription], 'Unknown') AS StudentEthnicityDescription
	   , Coalesce(stu.[IEPIndicator], 'Unknown') AS IEPIndicator
	   , Coalesce(stu.[LEPIndicator], 'Unknown') AS LEPIndicator
	   , Coalesce(stu.[Section504Indicator], 'Unknown') AS section504Indicator
	   , Coalesce(ed.[EducationOrganizationShortName], 'Unknown') AS EducationOrganizationShortName
	   , Coalesce(ed.[SchoolCategoryDescription], 'Unknown') AS SchoolCategoryDescription
	   , Coalesce(ed.[AcademicOrganizationalUnitDescription], 'Unknown') AS AcademicOrganizationalUnitDescription
	   , Coalesce(ed.[TrusteeDistrict], 'Unknown') AS TrusteeDistrict
	   , Coalesce(ed.[TitleIIndicator], 'Unknown') AS TitleIIndicator
	   , Coalesce(ed.[EducationOrganizationMagnetIndicator], 'Unknown') AS EducationOrganizationMagnetIndicator
	   , Coalesce(ed.[YearRoundIndicator], 'Unknown') AS YearRoundIndicator
	   , Case 
			when s.QuestionNumber IN (Select Distinct ItemNumber
					From dws.LongTextResponseStudent2016_backup r
					Where r.ResponseNumber = '3' AND r.ResponseText = '' ) AND s.ResponseNumber IN('4','5') 
				then CAST((s.[ResponseNumber] - 1) AS nvarchar)
			else s.[ResponseNumber] 
			end as responseIndicator
	   , Coalesce(s.[QuestionNumber], 'Unknown') AS QuestionNumber
	   , Coalesce(r.[ItemText], 'No response') AS ItemText
	   , Coalesce(s.[ResponseNumber], 'No response') AS responseValue
	   , Coalesce(r.[ResponseText], 'No response') AS responseLabel
	   , rq.[Student] AS Stu
	   , rq.[Parent] AS Par
	   , rq.[Staff] AS Staff
	   , Coalesce(rq.[Category], 'Unknown') AS Category
	   , Coalesce(rq.[questiontext], 'No response') AS questiontext
FROM dws.LongStudentSurvey2016_backup s
LEFT JOIN dws.LongTextResponseStudent2016_backup r
ON s.QuestionNumber=r.ItemNumber AND s.ResponseNumber=r.ResponseNumber
LEFT JOIN sdm.dbo.DimStudent stu
ON stu.[StudentNumber]=s.[Student ID Number] AND s.[Date Submitted] >= stu.[StudentRowEffectiveDate]
AND s.[Date Submitted] <= Stu.[StudentRowExpirationDate]
LEFT JOIN sdm.curr.DimEducationOrganization ed
ON ed.[EducationOrganizationID] = s.[Student School Site Code]
LEFT JOIN dws.RelatedQuestions2016 rq
ON rq.[Student] = s.[QuestionNumber] 
UNION
SELECT 'DWS' AS SurveyFamily
     , 'Staff' AS SurveyTitle
	 , '2016' AS SurveyYear
	 , '0' AS SurveyVersion
	 , Coalesce(s.[ID #], 'Unknown') AS surveyid
	 , Coalesce(s.[Date Started], 'Unknown') AS SurveyDate
	 , Coalesce(s.[Staff Location Code], 'Unknown') AS Schoolid
	 , Coalesce(ed.[EducationOrganizationShortName], 'Unknown') AS SchoolName
	 , Coalesce(s.[Submitter IP Address], 'Unknown') AS IP
	 , 'Unknown' AS studentid 
	 , 'Unknown' AS bdate
	 , Coalesce(s.[Response Language], 'Unknown') AS SurveyLanguage
	 , Coalesce(s.[Question 0], 'Unknown') AS Parent
	 , 'Unknown' AS gradeLevel
	 , Coalesce(s.[Time Started], 'Unknown') AS starttime
	 , Coalesce(s.[Time Submitted], 'Unknown') AS endtime
	 , datediff(ss,s.[Time Started],s.[Time Submitted])/60.0 AS [minutesToComplete]
	 , Coalesce(s.[ResponseNumber], 'No response') AS responses
	 , Coalesce(s.[QuestionNumber], 'Unknown') AS questions
	 , 'Unknown' AS StudentGenderDescription
	 , 'Unknown' AS StudentEthnicityDescription
	 , 'Unknown' AS IEPIndicator
	 , 'Unknown' AS LEPIndicator
	 , 'Unknown' AS section504indicator
	 , Coalesce(ed.[EducationOrganizationShortName], 'Unknown') AS EducationOrganizationShortName
	 , Coalesce(ed.[SchoolCategoryDescription], 'Unknown') AS SchoolCategoryDescription
	 , Coalesce(ed.[AcademicOrganizationalUnitDescription], 'Unknown') AS AcademicOrganizationalUnitDescription
	 , Coalesce(ed.[TrusteeDistrict], 'Unknown') AS TrusteeDistrict
	 , Coalesce(ed.[TitleIIndicator], 'Unknown') AS TitleIIndicator
	 , Coalesce(ed.[EducationOrganizationMagnetIndicator], 'Unknown') AS EducationOrganizationMagnetIndicator
	 , Coalesce(ed.[YearRoundIndicator], 'Unknown') AS YearRoundIndicator
	 , Case 
			when s.QuestionNumber IN (Select Distinct ItemNumber
					From dws.LongTextResponseStudent2016_backup r
					Where r.ResponseNumber = '3' AND r.ResponseText = '' ) AND s.ResponseNumber IN('4','5') 
				then CAST((s.[ResponseNumber] - 1) AS nvarchar)
			else s.[ResponseNumber] 
			end as responseIndicator
	 , Coalesce(s.[QuestionNumber], 'Unknown') AS ItemNumber
	 , Coalesce(r.[ItemText], 'No response') AS ItemText
	 , Coalesce(s.[ResponseNumber], 'No response') AS responseValue
	 , Coalesce(r.[ResponseText], 'No response') AS responseLabel
	 , rq.[Student] AS Stu
	 , rq.[Parent] AS Par
	 , rq.[Staff] AS Staff
	 , Coalesce(rq.[Category], 'Unknown') AS Category
	 , Coalesce(rq.[questiontext], 'No response') AS questiontext
FROM dws.LongStaffSurvey2016_backup s
LEFT JOIN dws.LongTextResponseSchoolStaff2016_backup r
ON s.QuestionNumber=r.ItemNumber AND s.ResponseNumber=r.ResponseNumber
LEFT JOIN sdm.curr.DimEducationOrganization ed
ON ed.[EducationOrganizationID] = s.[Staff Location Code]
LEFT JOIN dws.RelatedQuestions2016 rq
ON rq.[Staff] = s.[QuestionNumber] 
) TablesJoined
