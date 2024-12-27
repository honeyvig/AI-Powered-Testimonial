# AI-Powered-Testimonial
we have an online survey. see below. When someone completes the survey I want AI to rewrite it into a testimonial.

(link removed)

DETAIL

1. Client completes survey then clicks on NEXT button
2. In the background AI converts the survey into a 1 paragraph testimonial ( see sample below ) then displays for person to read
3. Below the new testimonial are buttons EDIT- APPROVE - REDO - CANCEL

SAMPLE:
:
This was created by the web based form:

Name * Sarah Zuk
What company are you with? Or, which client did we represent? *
CSI
Event Start Date Monday, September 9, 2024
Time it took to reply to your inquiry.
Satisfied
How was your experience on the phone with a colleague?
Satisfied
Time it took to get your quote.
Satisfied
Arrived on time
Satisfied
Setup on time
Satisfied
Started on time
Satisfied
Apperance of staff
Satisfied
Staff professionalism
Satisfied
Quality of personalization
Satisfied
Quality of Swag product
Satisfied
Flow of event
Satisfied
Organization
Satisfied
Reaction of attendees
Satisfied
Overall, how satisfied were you with our services at your event?
Satisfied
Overall, how satisified were you with our communication and planning process leading up to the event?
Satisfied
Overall, how satisfied were you with our team's professionalism and performance on the day of the event?
Satisfied
Overall, how satisified were you with the quality of the services provided (e.g., booth set-up, product customization, customer engagement)?
Satisfied
Would you consider booking us again for future events?
Yes
I agree to having my testimonial shared on Digital Event's website and promotional materials.
Yes

AI TESTIMONIAL WRITTEN USING THE ABOVE SURVEY:

"We had a fantastic experience with Digital Events for our recent event at CSI on September 9, 2024. From the initial inquiry to the day of the event, every aspect of their service was handled professionally and efficiently. The team was responsive and attentive throughout the planning process, and on the event day, they arrived on time, set up seamlessly, and engaged our attendees with high-quality, personalized swag. The staff's professionalism and the event's organization were impressive, making everything run smoothly. We were very satisfied with their services and would definitely consider booking them again for future events." – Sarah Zuk, CSI
---------
To achieve this functionality, we will need to create a Python script that utilizes AI (specifically OpenAI's GPT-3/4 API or a similar language model) to convert survey responses into a coherent testimonial. The AI model will take the responses from the survey form and rewrite it into a testimonial-like paragraph, which will be displayed for the user to approve, edit, or cancel.

Here's a breakdown of the solution:

    Survey Submission: Once a user completes the survey and clicks "Next," the survey responses are sent to the backend.
    AI Processing: The backend uses the AI to generate a testimonial based on the survey responses.
    Display & Options: The AI-generated testimonial is displayed, and the user can choose to edit, approve, redo, or cancel.

Python Code for Backend:

The following Python code uses the OpenAI GPT API to generate the testimonial. It also implements basic logic to allow the user to either accept, edit, redo, or cancel the testimonial.

import openai

# Set your OpenAI API key
openai.api_key = 'your-openai-api-key'

# Function to generate testimonial based on survey data
def generate_testimonial(survey_data):
    # Construct the prompt based on the survey data
    prompt = f"""
    Based on the following survey responses, generate a professional and concise testimonial:
    
    Name: {survey_data['name']}
    Company: {survey_data['company']}
    Event Date: {survey_data['event_date']}
    Time it took to reply to your inquiry: {survey_data['inquiry_time']}
    Phone experience: {survey_data['phone_experience']}
    Time to get quote: {survey_data['quote_time']}
    Arrival on time: {survey_data['arrival_time']}
    Setup on time: {survey_data['setup_time']}
    Started on time: {survey_data['started_time']}
    Appearance of staff: {survey_data['staff_appearance']}
    Staff professionalism: {survey_data['staff_professionalism']}
    Quality of personalization: {survey_data['personalization_quality']}
    Quality of swag product: {survey_data['swag_quality']}
    Flow of event: {survey_data['event_flow']}
    Organization: {survey_data['organization']}
    Reaction of attendees: {survey_data['attendee_reaction']}
    Overall satisfaction with services: {survey_data['overall_satisfaction']}
    Satisfaction with communication and planning: {survey_data['comm_planning_satisfaction']}
    Satisfaction with professionalism on the event day: {survey_data['event_professionalism_satisfaction']}
    Satisfaction with service quality: {survey_data['service_quality_satisfaction']}
    Would you book again: {survey_data['would_book_again']}
    
    Use these survey responses to write a testimonial in a friendly, positive tone. The testimonial should focus on the overall experience, including the professionalism, quality of service, and satisfaction.
    """

    # Make API call to OpenAI to generate the testimonial
    response = openai.Completion.create(
        engine="text-davinci-003",  # You can use another engine like "gpt-4" if available
        prompt=prompt,
        max_tokens=200,
        temperature=0.7
    )

    # Extract the generated testimonial from the response
    testimonial = response.choices[0].text.strip()
    return testimonial

# Example survey data (this would come from your survey form)
survey_data = {
    'name': 'Sarah Zuk',
    'company': 'CSI',
    'event_date': 'Monday, September 9, 2024',
    'inquiry_time': 'Satisfied',
    'phone_experience': 'Satisfied',
    'quote_time': 'Satisfied',
    'arrival_time': 'Satisfied',
    'setup_time': 'Satisfied',
    'started_time': 'Satisfied',
    'staff_appearance': 'Satisfied',
    'staff_professionalism': 'Satisfied',
    'personalization_quality': 'Satisfied',
    'swag_quality': 'Satisfied',
    'event_flow': 'Satisfied',
    'organization': 'Satisfied',
    'attendee_reaction': 'Satisfied',
    'overall_satisfaction': 'Satisfied',
    'comm_planning_satisfaction': 'Satisfied',
    'event_professionalism_satisfaction': 'Satisfied',
    'service_quality_satisfaction': 'Satisfied',
    'would_book_again': 'Yes'
}

# Generate testimonial
testimonial = generate_testimonial(survey_data)
print(f"Generated Testimonial: {testimonial}")

Explanation of the Code:

    OpenAI API Integration:
        We use the OpenAI API to generate a testimonial based on the provided survey responses.
        The generate_testimonial function receives the survey data as a dictionary, and constructs a prompt for the AI to generate the testimonial.

    Survey Data:
        This dictionary simulates the survey data the user submits. In your actual implementation, this data would come from the survey form that the user fills out.

    AI Model (GPT-3/4):
        We use OpenAI's GPT-3/4 (or any other generative AI model) to process the survey data and generate the testimonial.
        The response from the model will be a concise and professional paragraph, which serves as the testimonial.

Example of the Generated Testimonial:

Based on the sample input, the AI-generated testimonial might look like this:

"We had a fantastic experience with Digital Events for our recent event at CSI on September 9, 2024. From the initial inquiry to the day of the event, every aspect of their service was handled professionally and efficiently. The team was responsive and attentive throughout the planning process, and on the event day, they arrived on time, set up seamlessly, and engaged our attendees with high-quality, personalized swag. The staff's professionalism and the event's organization were impressive, making everything run smoothly. We were very satisfied with their services and would definitely consider booking them again for future events." – Sarah Zuk, CSI

Displaying the Testimonial and User Interaction:

Once the AI generates the testimonial, the following steps can be taken in the web application:

    Display the Testimonial: After the user clicks "Next," the testimonial is displayed on the page.
    Buttons for User Interaction: Below the testimonial, display buttons:
        Edit: Allows the user to modify the testimonial.
        Approve: Approves the testimonial and stores it in the database.
        Redo: Regenerates the testimonial.
        Cancel: Cancels the process and returns the user to the previous screen.

The user interface and button logic can be implemented using JavaScript on the frontend and an appropriate backend framework (Flask, Django, etc.) to handle the interaction with the AI.
Example Frontend (HTML & JavaScript):

<div id="testimonial-container">
    <p id="generated-testimonial">
        <!-- The generated testimonial will be inserted here -->
    </p>
    <button id="edit-button">Edit</button>
    <button id="approve-button">Approve</button>
    <button id="redo-button">Redo</button>
    <button id="cancel-button">Cancel</button>
</div>

<script>
    // Example function to update the testimonial
    document.getElementById('generated-testimonial').innerText = "We had a fantastic experience with Digital Events for our recent event at CSI on September 9, 2024. ...";

    // Button click handlers
    document.getElementById('edit-button').onclick = function() {
        // Allow the user to edit the testimonial
        alert("Editing functionality");
    };
    document.getElementById('approve-button').onclick = function() {
        // Approve and store the testimonial in the database
        alert("Testimonial Approved");
    };
    document.getElementById('redo-button').onclick = function() {
        // Regenerate the testimonial
        alert("Regenerating Testimonial");
    };
    document.getElementById('cancel-button').onclick = function() {
        // Cancel the process
        alert("Process Cancelled");
    };
</script>

This setup will allow you to efficiently collect survey data, transform it into a professional testimonial using AI, and provide users with an interactive way to approve or modify the generated testimonial.
