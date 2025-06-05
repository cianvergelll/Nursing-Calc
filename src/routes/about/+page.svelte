<script>
    import { FontAwesomeIcon } from "@fortawesome/svelte-fontawesome";
    import Navbar from "../component/Navbar.svelte";

</script>

<Navbar />

<div class="w-[50%] flex flex-col mx-auto mb-10">
  <p class="font-bold text-3xl mt-8 ml-5">About Nurse Calc</p>
    <div class="w-full my-5 border border-gray-300 py-4 rounded-xl shadow-lg">
        <p class="text-lg ml-10 font-medium">Our Mission</p>
        <p class="text-s ml-10 text-gray-600 mb-5">Supporting nursing education and practice through reliable calculation tools</p>
        <p class="mx-10 text-medium mb-5">NurseCalc was developed to provide nursing students and professionals with accurate,<br> easy-to-use drug calculation tools. Our mission is to support safe medication administration practices through education and practical resources.
        <br><br>
        We believe that understanding the principles behind drug calculations is just as important as getting the right answer. That's why our tools include explanations of formulas and step-by-step guides to help users build confidence in their calculation skills.</p>
    </div>

    <div class="w-full my-5 border border-gray-300 py-4 rounded-xl shadow-lg">
        <p class="text-lg ml-10 font-medium">Educational Purpose</p>
        <p class="text-s ml-10 text-gray-600 mb-5">Important information about using NurseCalc</p>

        <div class="bg-sky-100 w-[90%] my-5 mx-auto rounded-lg flex flex-col px-5 py-5 border-l-4 border-sky-800">
            <p class="text-medium font-medium">NurseCalc is designed for educational purposes only. While we strive for accuracy, all calculations should be verified according to your institution's protocols.</p>
        </div>

        <p class="mx-10 text-medium mb-5">This tool is intended to serve as a learning aid and reference for nursing students and professionals. It should not replace critical thinking, professional judgment, or institutional policies regarding medication administration.</p>
    </div>



    <div class="w-full my-5 border border-gray-300 py-4 rounded-xl shadow-lg">
        <p class="text-lg ml-10 mb-5 font-medium">Disclaimer</p>
        <p class="text-s mx-10 text-gray-600 mb-5">NurseCalc is provided "as is" without warranty of any kind, express or implied. The creators and maintainers of NurseCalc do not assume any liability for the use or misuse of this tool. Users are solely responsible for verifying all calculations and following appropriate clinical guidelines and institutional policies.
        <br><br>
        This application is intended for educational purposes only and should not be the sole resource used for medication administration decisions. Always consult appropriate reference materials, follow your institution's protocols, and use professional judgment when administering medications.</p>
    </div>
</div>