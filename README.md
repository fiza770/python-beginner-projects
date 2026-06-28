# python-beginner-projects
My Python learning journey for scholarship applications
# student_scholarship_matcher.py
# By Fiza - Scholarship Portfolio Project

# =====================
# FUNCTIONS
# =====================

def get_student_info():
    print("=" * 40)
    print("   🎓 STUDENT SCHOLARSHIP MATCHER")
    print("=" * 40)
    
    name = input("\nEnter your name: ")
    age = int(input("Enter your age: "))
    country = input("Enter your country: ")
    grade = float(input("Enter your GPA/percentage: "))
    
    # Tuple - personal info that won't change
    personal_info = (name, age, country)
    
    return personal_info, grade


def get_subjects():
    subjects = []
    print("\nEnter your subjects (type 'done' to finish):")
    
    while True:
        subject = input("Subject: ").strip()
        if subject.lower() == "done":
            break
        subjects.append(subject)
    
    return subjects


def match_scholarships(grade, country):
    # Dictionary of scholarships
    scholarships = {
        "Fulbright": {
            "min_grade": 80,
            "countries": ["pakistan", "india", "bangladesh"],
            "field": "Any field",
            "deadline": "December 2025"
        },
        "Chevening UK": {
            "min_grade": 75,
            "countries": ["pakistan", "nigeria", "kenya"],
            "field": "Leadership & Any field",
            "deadline": "November 2025"
        },
        "DAAD Germany": {
            "min_grade": 70,
            "countries": ["pakistan", "india", "egypt"],
            "field": "Engineering & Sciences",
            "deadline": "October 2025"
        },
        "Turkish Government": {
            "min_grade": 65,
            "countries": ["pakistan", "afghanistan", "somalia"],
            "field": "Any field",
            "deadline": "February 2026"
        }
    }
    
    matched = []
    
    for name, details in scholarships.items():
        if grade >= details["min_grade"] and country.lower() in details["countries"]:
            matched.append({
                "name": name,
                "field": details["field"],
                "deadline": details["deadline"]
            })
    
    return matched


def show_results(personal_info, grade, subjects, matched):
    name, age, country = personal_info  # unpacking tuple
    
    print("\n" + "=" * 40)
    print("         📋 YOUR PROFILE SUMMARY")
    print("=" * 40)
    print(f"Name:      {name}")
    print(f"Age:       {age}")
    print(f"Country:   {country}")
    print(f"Grade:     {grade}%")
    
    print("\n📚 Your Subjects:")
    for i, subject in enumerate(subjects, 1):
        print(f"   {i}. {subject}")
    
    print("\n🏆 Matched Scholarships:")
    print("-" * 40)
    
    if matched:
        for s in matched:
            print(f"\n✅ {s['name']}")
            print(f"   Field:    {s['field']}")
            print(f"   Deadline: {s['deadline']}")
    else:
        print("❌ No matches found. Try improving your grade!")
    
    print("\n" + "=" * 40)
    
    # Conditional message based on grade
    if grade >= 80:
        print("🌟 Excellent! You qualify for top scholarships!")
    elif grade >= 70:
        print("👍 Good standing! Keep improving your profile.")
    elif grade >= 60:
        print("📈 Work on your grades to unlock more options.")
    else:
        print("💪 Keep studying! Every improvement counts.")


# =====================
# MAIN PROGRAM
# =====================

personal_info, grade = get_student_info()
subjects = get_subjects()
matched = match_scholarships(grade, personal_info[2])
show_results(personal_info, grade, subjects, matched)