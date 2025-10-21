module occ_minimal (
  input wire test_mode,      // 1: test mode, 0: functional
  input wire atspeed_mode,   // 1: at-speed capture, 0: shift
  input wire shift_en,       // scan shift enable
  input wire scan_clk,       // scan clock
  input wire func_clk,       // functional clock
  output wire occ_clk        // output controlled clock
);

reg [3:0] shift_reg;
reg cg_en;
reg occ_clk_int;

// Shift register to generate capture pulse timing
always @(posedge func_clk or posedge test_mode) begin
  if (test_mode)
    shift_reg <= {shift_reg[2:0], ~shift_en};
  else
    shift_reg <= 0;
end

// Clock gate enable logic
always @(*) begin
  if (~test_mode)
    cg_en = 1'b1;
  else begin
    if (atspeed_mode)
      cg_en = ~shift_reg[3] & shift_reg[1];
    else
      cg_en = ~shift_reg[3] & shift_reg[2];
  end
end

// Clock mux gating
always @(posedge func_clk or posedge scan_clk) begin
  if (test_mode) begin
    if (shift_en)
      occ_clk_int <= scan_clk;
    else
      occ_clk_int <= func_clk & cg_en;
  end else begin
    occ_clk_int <= func_clk;
  end
end

assign occ_clk = occ_clk_int;

endmodule