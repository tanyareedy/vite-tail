<template>
  <div ref="document" class="p-20 ">
    <button
      class="bg-green-400 rounded-full p-1 text-xs text-white m-2"
      @click="exportToPDF"
    >
      Export to PDF
    </button>

    <div class="border-line">
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
                    <h5>{{ companyInfo.poBox }}</h5>
                    <h5>{{ companyInfo.country }}</h5>
                    <h5>Phone No: {{ companyInfo.phoneNo }}</h5>
                    <h5>Email:{{ companyInfo.email }}</h5>
                    <h5>VAT Registration No:{{ companyInfo.vatReg }}</h5>
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

        <section>
          <div>
            <div>itme</div>
            <div>
              <div>ite,</div>
              <div>ite,</div>
            </div>
          </div>
        </section>
        <!--    company information -->
      </main>

      <img class="mt-40" src="@/assets/processed.jpeg" />xw
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
  @apply border border-2 border-indigo-100;
}
</style>
