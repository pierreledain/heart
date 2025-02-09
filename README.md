<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Medical Practice Test</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
        }
        .question-container {
            margin-bottom: 20px;
            padding: 15px;
            border: 1px solid #ddd;
            border-radius: 5px;
        }
        .options {
            margin: 10px 0;
        }
        .option {
            margin: 5px 0;
        }
        button {
            padding: 8px 16px;
            margin: 5px;
            cursor: pointer;
        }
        #feedback {
            margin-top: 10px;
            padding: 10px;
            border-radius: 5px;
        }
        .correct {
            background-color: #d4edda;
            border: 1px solid #c3e6cb;
        }
        .incorrect {
            background-color: #f8d7da;
            border: 1px solid #f5c6cb;
        }
    </style>
</head>
<body>
    <div id="main-container">
        <div class="question-container">
            <h3 id="question-number"></h3>
            <div id="question-text"></div>
            <div class="options" id="options"></div>
            <button onclick="submitAnswer()">Submit</button>
            <button onclick="nextQuestion()" id="next-btn" style="display: none;">Next Question</button>
            <div id="feedback"></div>
        </div>
    </div>

    <script>
        const questions = [
            {
                question: "Which part of the heart is primarily formed by the left atrium and receives the pulmonary veins and the superior and inferior vena cava?",
                options: ["A) Apex", "B) Coronary sulcus", "C) Anterior interventricular sulcus", "D) Base"],
                correct: "D",
                explanation: "The base of the heart is primarily formed by the left atrium and receives the pulmonary veins and the superior and inferior vena cava."
            },
            {
                question: "Which part of the mediastinum is located between the transverse thoracic plane and the diaphragm?",
                options: ["A) Superior mediastinum", "B) Inferior mediastinum", "C) Anterior mediastinum", "D) Middle mediastinum"],
                correct: "B",
                explanation: "The inferior mediastinum is located between the transverse thoracic plane and the diaphragm."
            },
            {
                question: "What is the term for the closure of the tricuspid and mitral valves after the emptying of the atria?",
                options: ["A) 1st sound (lub)", "B) 2nd sound (dub)", "C) 3rd sound", "D) 4th sound"],
                correct: "A",
                explanation: "The 1st heart sound (lub) is associated with the closure of the tricuspid and mitral valves after the emptying of the atria, marking the beginning of systole."
            },
            {
                question: "Which cavity does the mediastinum occupy within the body?",
                options: ["A) Cranial cavity", "B) Abdominal cavity", "C) Thoracic cavity", "D) Pelvic cavity"],
                correct: "C",
                explanation: "The mediastinum occupies the central compartment of the thoracic cavity."
            },
            {
                question: "Which part of the mediastinum contains the heart and the roots of its great vessels?",
                options: ["A) Superior mediastinum", "B) Anterior mediastinum", "C) Middle mediastinum", "D) Posterior mediastinum"],
                correct: "C",
                explanation: "The middle mediastinum contains the heart and the roots of its great vessels."
            },
            {
                question: "Which part of the mediastinum extends from the superior thoracic aperture to the horizontal plane formed by the sternal angle to the IV disk of T4 – T5?",
                options: ["A) Superior mediastinum", "B) Inferior mediastinum", "C) Anterior mediastinum", "D) Middle mediastinum"],
                correct: "A",
                explanation: "The superior mediastinum extends from the superior thoracic aperture to the mentioned horizontal plane."
            },
            {
                question: "Which layer of the heart also covers the heart valves?",
                options: ["A) Epicardium", "B) Myocardium", "C) Endocardium", "D) Pericardium"],
                correct: "C",
                explanation: "The endocardium, the thin internal layer of the heart, also covers the heart valves and lines the interior of the heart chambers."
            },
            {
                question: "Which part of the heart is primarily responsible for receiving oxygenated blood from the pulmonary veins?",
                options: ["A) Apex", "B) Base", "C) Right atrium", "D) Left atrium"],
                correct: "D",
                explanation: "The left atrium is primarily responsible for receiving oxygenated blood from the pulmonary veins."
            },
            {
                question: "Which layer of the serous pericardium lines the external surface of the heart and forms the epicardium?",
                options: ["A) Parietal layer", "B) Visceral layer", "C) Fibrous layer", "D) Endocardium"],
                correct: "B",
                explanation: "The visceral layer of the serous pericardium lines the external surface of the heart and forms the epicardium, which is the outermost layer of the heart wall."
            },
            {
                question: "What is the continuous inferior extension of the fibrous pericardium that attaches to the central tendon of the diaphragm?",
                options: ["A) Sternopericardial ligament", "B) Pericardiacophrenic ligament", "C) Pretracheal ligament", "D) Pulmonary trunk"],
                correct: "B",
                explanation: "The pericardiacophrenic ligament is the continuous inferior extension of the fibrous pericardium that attaches to the central tendon of the diaphragm."
            },
            {
                question: "Which artery accompanies the phrenic nerve to the diaphragm?",
                options: ["A) Brachiocephalic artery", "B) Pericardiophrenic artery", "C) Pulmonary artery", "D) Coronary artery"],
                correct: "B",
                explanation: "The pericardiophrenic artery is a branch of the internal thoracic artery that accompanies the phrenic nerve to the diaphragm."
            },
            {
                question: "What does the fibrous skeleton of the heart provide attachment for?",
                options: ["A) Valves", "B) Blood vessels", "C) Nerves", "D) Lungs"],
                correct: "A",
                explanation: "The fibrous skeleton of the heart provides attachments for the heart valves, ensuring their proper function and preventing their over-distention."
            },
            {
                question: "Which ligament attaches the fibrous pericardium anteriorly to the posterior surface of the sternum?",
                options: ["A) Sternopericardial ligament", "B) Pericardiacophrenic ligament", "C) Pretracheal ligament", "D) Diaphragmatic ligament"],
                correct: "A",
                explanation: "The sternopericardial ligament attaches the fibrous pericardium to the posterior surface of the sternum."
            },
            {
                question: "Where is the maximal sound of mitral valve closure heard on the chest wall?",
                options: ["A) Apex", "B) Base", "C) Inferolateral part of the left ventricle", "D) Anterior interventricular sulcus"],
                correct: "A",
                explanation: "The maximal sound of mitral valve closure is heard at the apex of the heart on the chest wall."
            },
            {
                question: "Which border of the heart extends between the superior vena cava (SVC) and the inferior vena cava (IVC)?",
                options: ["A) Right border", "B) Inferior border", "C) Left border", "D) Superior border"],
                correct: "A",
                explanation: "The right border of the heart extends between the superior vena cava (SVC) and the inferior vena cava (IVC)."
            },
            {
                question: "What clinical symptoms might a person with pericardial tamponade experience?",
                options: ["A) Increased appetite", "B) Fever and chills", "C) Shortness of breath and chest pain", "D) Visual disturbances"],
                correct: "C",
                explanation: "Common symptoms of pericardial tamponade include shortness of breath and chest pain, which result from the compression of the heart within the pericardial sac and reduced cardiac output."
            },
            {
                question: "Which part of the heart is primarily located on the diaphragmatic surface?",
                options: ["A) Right atrium", "B) Left atrium", "C) Right ventricle", "D) Left ventricle"],
                correct: "D",
                explanation: "The diaphragmatic surface of the heart is primarily occupied by the left ventricle, with a lesser contribution by the right ventricle."
            },
            {
                question: "What is the function of the oblique pericardial sinus?",
                options: ["A) Forming a pocket-like recess behind the right atrium", "B) Forming a pocket-like recess behind the left ventricle", "C) Forming a pocket-like recess behind the right ventricle", "D) Forming a pocket-like recess behind the left atrium"],
                correct: "D",
                explanation: "The oblique pericardial sinus is a pocket-like recess within the pericardial cavity formed by the left atrium. It serves as a blind sac and does not have a specific physiological function."
            },
            {
                question: "Which part of the heart remains motionless during the cardiac cycle and is posterior to the left 5th intercostal space?",
                options: ["A) Apex", "B) Base", "C) Inferolateral part of the left ventricle", "D) Anterior interventricular sulcus"],
                correct: "A",
                explanation: "The apex of the heart remains motionless during the cardiac cycle and is located posterior to the left 5th intercostal space."
            },
            {
                question: "Which surface of the heart is primarily occupied by the right atrium?",
                options: ["A) Anterior (sternocostal) surface", "B) Diaphragmatic (inferior) surface", "C) Right pulmonary surface", "D) Left pulmonary surface"],
                correct: "C",
                explanation: "The right pulmonary surface of the heart is primarily occupied by the right atrium."
            },
            {
                question: "What anatomical structure demarcates the atria from the ventricles on the external surface of the heart?",
                options: ["A) Apex", "B) Coronary sulcus", "C) Anterior interventricular sulcus", "D) Posterior interventricular sulcus"],
                correct: "B",
                explanation: "The coronary sulcus, also known as the atrioventricular groove, demarcates the atria from the ventricles on the external surface of the heart."
            },
            {
                question: "Which border of the heart is formed by the left ventricle and the left auricle?",
                options: ["A) Right border", "B) Inferior border", "C) Left border", "D) Superior border"],
                correct: "C",
                explanation: "The left border of the heart is formed by the left ventricle and the left auricle."
            },
            {
                question: "What material forms the fibrous skeleton of the heart?",
                options: ["A) Dense elastic cartilage", "B) Dense hyaline cartilage", "C) Dense cartilaginous rings", "D) Bone"],
                correct: "C",
                explanation: "The fibrous skeleton of the heart is formed of dense cartilaginous rings that surround the orifice of the valves."
            },
            {
                question: "In the pericardial cavity, which structure runs transversely between the aorta and pulmonary trunk, as well as the superior vena cava (SVC)?",
                options: ["A) Transverse pericardial sinus", "B) Peripheral pericardial sinus", "C) Oblique pericardial sinus", "D) Lateral pericardial sinus"],
                correct: "A",
                explanation: "The transverse pericardial sinus is a space within the pericardial cavity that runs transversely between the aorta and pulmonary trunk and the superior vena cava (SVC)."
            },
            {
                question: "What is the primary function of the sympathetic trunk in the context of the pericardium?",
                options: ["A) Transmitting sensory information", "B) Regulating heart rate", "C) Vasomotor control", "D) Controlling diaphragm movements"],
                correct: "C",
                explanation: "The sympathetic trunk is primarily responsible for vasomotor control, which includes regulating blood vessel constriction and dilation."
            },
            {
                question: "Which nerve is responsible for motor control of the diaphragm?",
                options: ["A) Vagus nerve", "B) Sympathetic trunk", "C) Phrenic nerve", "D) Brachial plexus"],
                correct: "C",
                explanation: "The phrenic nerve is responsible for motor control of the diaphragm, allowing for breathing."
            },
            {
                question: "Which nerves are responsible for transmitting sensory information from the pericardium, with pain being referred to the skin of dermatomes C3 – C5?",
                options: ["A) Phrenic nerve", "B) Sympathetic trunk", "C) Vagus nerve", "D) Brachial plexus"],
                correct: "A",
                explanation: "The phrenic nerve (C3 – C5) is responsible for transmitting sensory information from the pericardium, and pain is often referred to the skin of dermatomes C3 – C5."
            },
            {
                question: "Which vein is a tributary of the brachiocephalic (or internal thoracic) veins?",
                options: ["A) Pulmonary vein", "B) Pericardiophrenic vein", "C) Hepatic vein", "D) Renal vein"],
                correct: "B",
                explanation: "The pericardiophrenic vein is a tributary of the brachiocephalic (or internal thoracic) veins."
            },
            {
                question: "Which of the following heart sounds is associated with the closure of the semilunar valves?",
                options: ["A) 1st sound (lub)", "B) 2nd sound (dub)", "C) 3rd sound", "D) 4th sound"],
                correct: "B",
                explanation: "The 2nd heart sound (dub) is associated with the closure of the semilunar valves (aortic and pulmonary) after the emptying of the ventricles."
            },
            {
                question: "Which layer of the heart is composed of cardiac muscle tissue?",
                options: ["A) Epicardium", "B) Myocardium", "C) Endocardium", "D) Pericardium"],
                correct: "B",
                explanation: "The myocardium is the middle layer of the heart and is composed of cardiac muscle tissue responsible for contracting and pumping blood."
            },
            {
                question: "Which part of the heart borders both the right and left atria and includes the auricles of the atria?",
                options: ["A) Right border", "B) Inferior border", "C) Left border", "D) Superior border"],
                correct: "D",
                explanation: "The superior border of the heart is formed by both the right and left atria and includes the auricles of the atria."
            },
            {
                question: "Which surface of the heart is primarily occupied by the left ventricle and lesser contribution right atrium?",
                options: ["A) Anterior (sternocostal) surface", "B) Diaphragmatic (inferior) surface", "C) Right pulmonary surface", "D) Left pulmonary surface"],
                correct: "B",
                explanation: "The diaphragmatic (inferior) surface of the heart is primarily occupied by the left ventricle and the left atrium."
            },
            {
                question: "Which chamber of the heart serves as the exit point for blood into the aorta?",
                options: ["A) Right atrium", "B) Right ventricle", "C) Left atrium", "D) Left ventricle"],
                correct: "D",
                explanation: "The left ventricle pumps oxygenated blood into the aorta, which is the main artery that carries blood to the systemic circulation."
            },
            {
                question: "Through which vessel does the right ventricle of the heart pump blood?",
                options: ["A) Aorta", "B) Pulmonary trunk", "C) Superior Vena Cava (SVC)", "D) Inferior Vena Cava (IVC)"],
                correct: "B",
                explanation: "The right ventricle pumps deoxygenated blood into the pulmonary trunk, which carries it to the lungs for oxygenation."
            },
            {
                question: "Which of the following vessels serves as an entrance to the right atrium of the heart?",
                options: ["A) Pulmonary trunk", "B) Aorta", "C) Superior Vena Cava (SVC)", "D) Pulmonary veins"],
                correct: "C",
                explanation: "The Superior Vena Cava (SVC) is one of the major vessels that serves as an entrance to the right atrium of the heart, bringing deoxygenated blood from the upper part of the body."
            },
            {
                question: "What is the anterior wall of the right atrium characterized by?",
                options: ["A) Smooth and thin-walled surface", "B) Pectinate muscles", "C) Left AV orifice", "D) Pulmonary veins"],
                correct: "B",
                explanation: "The anterior wall of the right atrium is characterized by pectinate muscles, which are rough and muscular."
            },
            {
                question: "What is the posterior part of the right atrium called, where the SVC, and IVC open?",
                options: ["A) Pectinate muscles", "B) Right AV orifice", "C) Sinus venarum", "D) Left atrium"],
                correct: "C",
                explanation: "The posterior part of the right atrium, where the Superior Vena Cava (SVC), Inferior Vena Cava (IVC), and coronary sinus open, is called the sinus venarum."
            },
            {
                question: "Where is the auricle of the right atrium located?",
                options: ["A) Overlapping the aorta", "B) On the left side of the heart", "C) On the anterior surface of the heart", "D) Overlapping the ascending aorta"],
                correct: "D",
                explanation: "The auricle of the right atrium is located in a way that it overlaps the ascending aorta."
            },
            {
                question: "Which structure of the heart forms the right border of the heart?",
                options: ["A) Right ventricle", "B) Left atrium", "C) Right atrium", "D) Left ventricle"],
                correct: "C",
                explanation: "The right atrium forms the right border of the heart."
            },
            {
                question: "What is the external vertical groove that separates the smooth and rough parts of the right atrium called?",
                options: ["A) Crista terminalis", "B) SVC", "C) Oval fossa", "D) Sulcus terminalis"],
                correct: "D",
                explanation: "The sulcus terminalis is the external vertical groove that separates the smooth and rough parts of the right atrium."
            },
            {
                question: "Where does the Superior Vena Cava (SVC) open into the right atrium?",
                options: ["A) At the level of the 3rd costal cartilage", "B) At the level of the 5th costal cartilage", "C) At the level of the 7th costal cartilage", "D) At the level of the 9th costal cartilage"],
                correct: "A",
                explanation: "The Superior Vena Cava (SVC) opens into the superior part of the right atrium at the level of the 3rd costal cartilage."
            },
            {
                question: "Which part of the right ventricle is characterized by a smooth wall and serves as the outflow tract to the pulmonary trunk?",
                options: ["A) Supraventricular crest", "B) Trabeculae carneae", "C) Conus arteriosus", "D) Right AV orifice"],
                correct: "C",
                explanation: "The smooth-walled structure known as the conus arteriosus in the right ventricle serves as the outflow tract to the pulmonary trunk."
            },
            {
                question: "What is the thick muscular ridge in the right ventricle that separates the ridged muscular wall from the smooth wall of the conus arteriosus?",
                options: ["A) Conus arteriosus", "B) Trabeculae carneae", "C) Supraventricular crest", "D) Right AV orifice"],
                correct: "C",
                explanation: "The thick muscular ridge in the right ventricle that separates the ridged muscular wall from the smooth wall of the conus arteriosus is known as the supraventricular crest."
            },
            {
                question: "What is the smooth-walled structure that forms a superior narrowing of the right ventricle and leads into the pulmonary trunk?",
                options: ["A) Supraventricular crest", "B) Trabeculae carneae", "C) Conus arteriosus", "D) Right AV orifice"],
                correct: "C",
                explanation: "The smooth-walled structure that forms a superior narrowing of the right ventricle and leads into the pulmonary trunk is the conus arteriosus."
            },
            {
                question: "Which chamber of the heart forms the largest part of the anterior surface of the heart and almost the entire inferior border?",
                options: ["A) Left atrium", "B) Left ventricle", "C) Right atrium", "D) Right ventricle"],
                correct: "D",
                explanation: "The right ventricle forms the largest part of the anterior surface of the heart and almost the entire inferior border."
            },
            {
                question: "What is the name for the muscular projections in the right ventricle that have their base on the ventricular wall?",
                options: ["A) Tricuspid valve", "B) Moderator band", "C) Pulmonary valve", "D) Papillary muscle"],
                correct: "D",
                explanation: "Papillary muscles are conical muscular projections in the right ventricle with their base on the ventricular wall. They play a role in anchoring the tricuspid valve and preventing it from inverting into the right atrium during ventricular contraction."
            },
            {
                question: "What is the function of the septomarginal trabecula (moderator band) in the right ventricle?",
                options: ["A) To regulate heart rate", "B) To prevent overdistension of the right ventricle", "C) To separate the right atrium and right ventricle", "D) To carry oxygenated blood to the lungs"],
                correct: "B",
                explanation: "The septomarginal trabecula, also known as the moderator band, carries part of the right branch of the atrioventricular bundle and helps prevent overdistension of the right ventricle during contraction."
            },
            {
                question: "Which papillary muscle in the right ventricle is the largest and most prominent, arising from the anterior wall?",
                options: ["A) Posterior papillary muscle", "B) Septal papillary muscle", "C) Anterior papillary muscle", "D) Moderator band"],
                correct: "C",
                explanation: "The largest and most prominent papillary muscle in the right ventricle is the anterior papillary muscle, which arises from the anterior wall."
            },
            {
                question: "Which structure guards the right atrioventricular orifice in the right ventricle?",
                options: ["A) Pulmonary valve", "B) Tricuspid valve", "C) Mitral valve", "D) Aortic valve"],
                correct: "B",
                explanation: "The tricuspid valve guards the right atrioventricular orifice in the right ventricle."
            },
            {
                question: "All of these are true except: A) The left atrium forms most of the base of the heart. B) The left atrium receives the pairs of R. & L. pulmonary veins in its smooth muscle wall. C) The auricle of the left atrium is trabeculated with pectinate muscles. D) The left AV. orifice discharges low-oxygen blood into the left ventricle.",
                options: ["A) The left atrium forms most of the base of the heart.", "B) The left atrium receives the pairs of R. & L. pulmonary veins in its smooth muscle wall.", "C) The auricle of the left atrium is trabeculated with pectinate muscles.", "D) The left AV. orifice discharges low-oxygen blood into the left ventricle."],
                correct: "D",
                explanation: "The left atrium discharges high-oxygen blood into the left ventricle through the left atrioventricular (AV) orifice. The other statements are true: the left atrium forms most of the base of the heart, it receives the pairs of R. & L. pulmonary veins in its smooth muscle wall, and its auricle is trabeculated with pectinate muscles."
            },
            {
                question: "All of these are true except: A) The left ventricle forms the apex of the heart. B) The left ventricle performs more work than the right ventricle because of higher arterial pressure. C) Outflow from the left ventricle leaves superiorly and to the right, with the blood having a U-shape (180˚) trajectory inside the left ventricle. D) The left ventricle forms almost all of the anterior surface of the heart.",
                options: ["A) The left ventricle forms the apex of the heart.", "B) The left ventricle performs more work than the right ventricle because of higher arterial pressure.", "C) Outflow from the left ventricle leaves superiorly and to the right, with the blood having a U-shape (180˚) trajectory inside the left ventricle.", "D) The left ventricle forms almost all of the anterior surface of the heart."],
                correct: "D",
                explanation: "The left ventricle forms almost all of the posterior and diaphragmatic surfaces of the heart, but it does not form almost all of the anterior surface. The other statements are true: the left ventricle forms the apex of the heart, performs more work than the right ventricle due to higher arterial pressure, and has outflow that leaves superiorly and to the right with a U-shape trajectory inside the left ventricle."
            },
            {
                question: "True or False: The walls of the left ventricle are 2-3 times thicker than those of the right ventricle.",
                options: ["A) True", "B) False"],
                correct: "A",
                explanation: "This statement is true. The walls of the left ventricle are indeed thicker than those of the right ventricle because the left ventricle needs to generate higher pressure to pump blood into the systemic circulation."
            },
            {
                question: "True or False: The aortic vestibule in the left ventricle leads to the pulmonary valve.",
                options: ["A) True", "B) False"],
                correct: "B",
                explanation: "This statement is false. The aortic vestibule in the left ventricle leads to the aortic orifice and the aortic valve, not the pulmonary valve. The pulmonary valve is associated with the right ventricle."
            },
            {
                question: "True or False: The mitral valve is located posterior to the sternum at the level of the 4th costal cartilage.",
                options: ["A) True", "B) False"],
                correct: "B",
                explanation: "This statement is false. The mitral valve is not located posterior to the sternum. It is situated in the left ventricle and is positioned posterior to the sternum at the level of the 4th intercostal cartilage."
            },
            {
                question: "Match the definitions with the correct term: Definition 1: This artery, together with the RCA, is the 1st branch of the aorta and runs in the coronary sulcus. Definition 2: This branch of the L. coronary artery supplies areas of the ventricles along the anterior IV groove. Definition 3: This branch of the L. coronary artery follows the coronary sulcus along the left border to the posterior border of the heart. Definition 4: This branch of the L. coronary artery follows the left margin of the heart and supplies the L. ventricle.",
                options: ["A) LAD (Left Anterior Descending)", "B) Circumflex branch", "C) Left marginal branch", "D) L. coronary artery (RCA)"],
                correct: "D",
                explanation: "The L. coronary artery (RCA) is the 1st branch of the aorta and runs in the coronary sulcus. The LAD (Left Anterior Descending) branch supplies areas of the ventricles along the anterior IV groove. The Circumflex branch follows the coronary sulcus along the left border to the posterior border of the heart. The Left Marginal branch of the circumflex branch follows the left margin of the heart and supplies the left ventricle."
            },
            {
                question: "True or False: The middle cardiac vein accompanies the posterior IV branch, drains portions supplied by the RCA, and is a tributary of the great cardiac vein.",
                options: ["A) True", "B) False"],
                correct: "B",
                explanation: "This statement is false. The middle cardiac vein is a tributary of the coronary sinus, not the great cardiac vein."
            },
            {
                question: "True or False: The smallest cardiac veins drain the myocardium directly into heart chambers, chiefly the ventricles.",
                options: ["A) True", "B) False"],
                correct: "B",
                explanation: "This statement is false. The smallest cardiac veins primarily drain the myocardium directly into the heart chambers, chiefly the atria, not the ventricles."
            }
        ];

        let currentQuestion = 0;
        let selectedAnswer = null;

        function displayQuestion() {
            // Reset selection and feedback
            selectedAnswer = null;
            document.getElementById("feedback").innerHTML = '';
            document.getElementById("feedback").className = '';
            document.getElementById("next-btn").style.display = "none";
            
            // Update question number
            document.getElementById("question-number").textContent = `Question ${currentQuestion + 1} of ${questions.length}`;
            
            // Update question text
            document.getElementById("question-text").textContent = questions[currentQuestion].question;
            
            // Update options
            const optionsContainer = document.getElementById("options");
            optionsContainer.innerHTML = '';
            
            questions[currentQuestion].options.forEach((option, index) => {
                const div = document.createElement("div");
                div.className = "option";
                
                const input = document.createElement("input");
                input.type = "radio";
                input.name = "answer";
                input.value = String.fromCharCode(65 + index);
                input.onchange = () => selectedAnswer = input.value;
                
                const label = document.createElement("label");
                label.textContent = option;
                
                div.appendChild(input);
                div.appendChild(label);
                optionsContainer.appendChild(div);
            });
        }

        function submitAnswer() {
            if (!selectedAnswer) {
                alert("Please select an answer!");
                return;
            }

            const feedback = document.getElementById("feedback");
            const correctAnswer = questions[currentQuestion].correct;
            const isCorrect = selectedAnswer === correctAnswer;

            feedback.innerHTML = `
                <strong>${isCorrect ? "Correct!" : "Incorrect!"}</strong><br>
                ${questions[currentQuestion].explanation}
            `;
            feedback.className = isCorrect ? "correct" : "incorrect";
            
            // Show the Next button
            document.getElementById("next-btn").style.display = "inline-block";
        }

        function nextQuestion() {
            currentQuestion++;
            
            if (currentQuestion < questions.length) {
                displayQuestion();
            } else {
                alert("Test completed! Well done!");
                currentQuestion = 0;
                displayQuestion();
            }
        }

        // Initial question display
        displayQuestion();
    </script>
</body>
</html>
