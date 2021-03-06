<template>
  <div ref="document" class="p-20 ">
    <button
      class="bg-green-400 rounded-full p-1 text-xs text-white m-2"
      @click="exportToPDF"
    >
      Export to PDF
    </button>

    <div class="">
      <main class="bg-gray-50">
        <!--    company information -->
        <section class="grid grid-cols-3">
          <div class="col-span-2">
            <div class="grid grid-cols-2">
              <div class="border-line">
                <div class="p-2">
                  <h4 class="text-sm font-medium capitalize">
                    {{ companyInfo.address }}
                  </h4>
                  <div class="text-xs">
                    <ul class="space-y-2">
                      <li>{{ companyInfo.poBox }}</li>
                      <li>{{ companyInfo.country }}</li>
                      <li>Phone No: {{ companyInfo.phoneNo }}</li>
                      <li>Email:{{ companyInfo.email }}</li>
                      <li>VAT Registration No:{{ companyInfo.vatReg }}</li>
                    </ul>
                  </div>
                </div>
              </div>
              <div class="border-line ">
                <div class="flex flex-col spac items-center">
                  <div class=" bg-red-500">
                    <svg
                      class="barcode"
                      :jsbarcode-format="item.format"
                      :jsbarcode-value="item.value"
                      jsbarcode-textmargin="0"
                      jsbarcode-fontoptions="bold"
                    ></svg>
                  </div>
                  <div>
                    <h1>
                      DUTY & TAX INVOICE
                    </h1>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="pl-10">Company Logo</div>
        </section>
        <!--    company information -->

        <!--        customer information-->
        <section class="">
          <div class="grid grid-cols-3 border-line p-2">
            <div class="col-span-2 text-sm">
              <h3 class="uppercase">{{ customerInfo.fullname }}</h3>
              <h3 class="uppercase w-44">{{ customerInfo.address }}</h3>
              <p class="pt-8">{{ customerInfo.phone }}</p>
            </div>
            <div class="text-sm">
              <table>
                <tr>
                  <td class="pr-8">Account Number</td>
                  <td>:DUTYAEDTU</td>
                </tr>
                <tr>
                  <td>Invoice Number</td>
                  <td>:D06981204</td>
                </tr>
                <tr>
                  <td>HWB Number</td>
                  <td>:2649676901</td>
                </tr>
                <tr>
                  <td>Date</td>
                  <td>17/02/2021</td>
                </tr>
                <tr>
                  <td>payment Due Date</td>
                  <td>17/02/2021</td>
                </tr>
              </table>
            </div>
          </div>
        </section>
        <!--        customer information-->

        <!--        shipment details-->
        <section class="py-1">
          <p class="text-center">
            Please Reimburse the Total Charges Shown Below To:
            {{ companyInfo.address }}
          </p>
          <div class="border-line">
            <h2 class="text-center font-medium text-xl">Shipment Details</h2>
          </div>
          <div class="border-line">
            <div class="p-10"></div>
          </div>
        </section>
        <!--        shipment details-->
      </main>

      <img class="mt-10" src="@/assets/processed.jpeg" />xw
    </div>
  </div>
</template>

<script>
import JsBarcode from "jsbarcode";
import html2pdf from "html2pdf.js";
export default {
  data() {
    return {
      companyInfo: {
        address: "DHL WORLDWIDE EXPRESS (DUBAI) LLC",
        poBox: "P.O. Box: 6252",
        country: "United Arab Emirates",
        phoneNo: "+971 2 426905",
        email: "billing-query.ae@dhl.com",
        vatReg: "100255554600003"
      },
      customerInfo: {
        fullname: "Ronald Weasely",
        address: `Jumeira village circle (JVC) UAE DUBAI`,
        phone: "+971 2 426905"
      },
      item: { format: "auto", value: 1610233004732, height: 5 }
    };
  },

  methods: {
    exportToPDF() {
      html2pdf(this.$refs.document, {
        margin: 1,
        filename: "document.pdf",
        image: { type: "jpeg", quality: 0.98 },
        html2canvas: { dpi: 192, letterRendering: true },
        jsPDF: { unit: "in", format: "a4", orientation: "portrait" }
      });
    }
  },
  mounted() {
    JsBarcode(".barcode").init();
  }
};
</script>

<style scoped>
.border-line {
  @apply border border-2 border-gray-600;
}
</style>
